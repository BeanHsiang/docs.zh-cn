---
title: 了解如何使用指数退避算法实现自定义 HTTP 调用重试
description: 了解如何使用指数退避算法从头实现 HTTP 调用重试，以处理可能的 HTTP 故障情况。
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/16/2018
ms.openlocfilehash: fdbc09cddde34cb8897e1d5b105cb15c863b59ce
ms.sourcegitcommit: 542aa405b295955eb055765f33723cb8b588d0d0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2019
ms.locfileid: "54362244"
---
# <a name="explore-custom-http-call-retries-with-exponential-backoff"></a>了解如何使用指数退避算法实现自定义 HTTP 调用重试

若要创建复原微服务，需要处理可能的 HTTP 故障情况。 处理此类故障的一种方法是，使用指数退避算法创建自己的重试实现（但不建议这样做）。

**重要说明：** 本部分说明如何创建自定义代码以实现 HTTP 调用重试。 但是不建议自己完成此过程，而是使用更加强大、可靠且更加简单易用的机制，如具有 Polly 的 `HttpClientFactory`（自 .NET Core 2.1 起可用）。 后续部分将介绍建议采用的方法。

作为初始探索，可以使用针对指数退避算法（如 [RetryWithExponentialBackoff.cs](https://gist.github.com/CESARDELATORRE/6d7f647b29e55fdc219ee1fd2babb260) 中所述）的实用工具类和如下所示的代码来实现自己的代码。

```csharp
public sealed class RetryWithExponentialBackoff
{
    private readonly int maxRetries, delayMilliseconds, maxDelayMilliseconds;

    public RetryWithExponentialBackoff(int maxRetries = 50,
        int delayMilliseconds = 200,
        int maxDelayMilliseconds = 2000)
    {
        this.maxRetries = maxRetries;
        this.delayMilliseconds = delayMilliseconds;
        this.maxDelayMilliseconds = maxDelayMilliseconds;
    }

    public async Task RunAsync(Func<Task> func)
    {
        ExponentialBackoff backoff = new ExponentialBackoff(this.maxRetries,
            this.delayMilliseconds,
            this.maxDelayMilliseconds);
        retry:
        try
        {
            await func();
        }
        catch (Exception ex) when (ex is TimeoutException ||
            ex is System.Net.Http.HttpRequestException)
        {
            Debug.WriteLine("Exception raised is: " +
                ex.GetType().ToString() +
                " –Message: " + ex.Message +
                " -- Inner Message: " +
                ex.InnerException.Message);
            await backoff.Delay();
            goto retry;
        }
    }
}

public struct ExponentialBackoff
{
    private readonly int m_maxRetries, m_delayMilliseconds, m_maxDelayMilliseconds;
    private int m_retries, m_pow;

    public ExponentialBackoff(int maxRetries, int delayMilliseconds,
        int maxDelayMilliseconds)
    {
        m_maxRetries = maxRetries;
        m_delayMilliseconds = delayMilliseconds;
        m_maxDelayMilliseconds = maxDelayMilliseconds;
        m_retries = 0;
        m_pow = 1;
    }

    public Task Delay()
    {
        if (m_retries == m_maxRetries)
        {
            throw new TimeoutException("Max retry attempts exceeded.");
        }
        ++m_retries;
        if (m_retries < 31)
        {
            m_pow = m_pow << 1; // m_pow = Pow(2, m_retries - 1)
        }
        int delay = Math.Min(m_delayMilliseconds * (m_pow - 1) / 2,
            m_maxDelayMilliseconds);
        return Task.Delay(delay);
    }
}
```

在客户端 C\# 应用程序（另一个 Web API 客户端微服务、ASP.NET MVC 应用程序，甚至 C\# Xamarin 应用程序）中使用此代码非常简单。 下面的示例使用 HttpClient 类演示操作方法。

```csharp
public async Task<Catalog> GetCatalogItems(int page,int take, int? brand, int? type)
{
    _apiClient = new HttpClient();
    var itemsQs = $"items?pageIndex={page}&pageSize={take}";
    var filterQs = "";
    var catalogUrl = $"{_remoteServiceBaseUrl}items{filterQs}?pageIndex={page}&pageSize={take}";
    var dataString = "";
    //
    // Using HttpClient with Retry and Exponential Backoff
    //
    var retry = new RetryWithExponentialBackoff();
    await retry.RunAsync(async () =>
    {
        // work with HttpClient call
        dataString = await _apiClient.GetStringAsync(catalogUrl);
    });
    return JsonConvert.DeserializeObject<Catalog>(dataString);
}
```

请记住，此代码仅适合用作概念证明。 以下部分介绍如何通过使用 HttpClientFactory 来应用更高级但却更简单的方法。 自 .NET Core 2.1 起可使用 HttpClientFactory，并提供 Polly 等经验证的复原库。

>[!div class="step-by-step"]
>[上一页](implement-resilient-entity-framework-core-sql-connections.md)
>[下一页](use-httpclientfactory-to-implement-resilient-http-requests.md)