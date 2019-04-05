---
title: 如何：设置 Windows 窗体 ProgressBar 控件显示的值
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ProgressBar control [Windows Forms], setting value displayed
- progress controls [Windows Forms], setting value displayed
ms.assetid: 0e5010ad-1e9a-4271-895e-5a3d24d37a26
ms.openlocfilehash: a889d6e5cd40833353c1b294031621b7b289ac4d
ms.sourcegitcommit: 160a88c8087b0e63606e6e35f9bd57fa5f69c168
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2019
ms.locfileid: "57715888"
---
# <a name="how-to-set-the-value-displayed-by-the-windows-forms-progressbar-control"></a>如何：设置 Windows 窗体 ProgressBar 控件显示的值
> [!IMPORTANT]
>  
  <xref:System.Windows.Forms.ToolStripProgressBar> 控件取代了 <xref:System.Windows.Forms.ProgressBar> 控件并添加了功能；但是，可以选择保留 <xref:System.Windows.Forms.ProgressBar> 控件以实现向后兼容并供将来使用。  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]提供了几个不同的方式来显示内的给定的值<xref:System.Windows.Forms.ProgressBar>控件。 你选择哪种方法取决于手头的任务或要解决此问题。 下表显示可以选择的方法。  
  
|方法|描述|  
|--------------|-----------------|  
|值设置<xref:System.Windows.Forms.ProgressBar>直接控制。|您知道会涉及，例如，在从数据源中读取记录的测量项总计，此方法非常有用的任务。 此外，如果您只需将值设置一次或两次，这是执行此操作的简单办法。 最后，使用此过程，如果需要减少显示进度条的值。|  
|增加<xref:System.Windows.Forms.ProgressBar>显示按固定值。|在显示的最小值和最大值，例如运行时间或已知总共已处理的文件数之间的简单计数时，此方法非常有用。|  
|增加<xref:System.Windows.Forms.ProgressBar>显示各不相同的值。|当您需要更改显示的值在不同的金额中次数时，此方法非常有用。 示例会显示一系列文件写入磁盘时已使用的硬盘空间量。|  
  
 若要设置由一个进度栏显示的值的最直接方式是通过设置<xref:System.Windows.Forms.ProgressBar.Value%2A>属性。 这可以在设计时或在运行时。  
  
### <a name="to-set-the-progressbar-value-directly"></a>若要直接设置 ProgressBar 值  
  
1.  设置<xref:System.Windows.Forms.ProgressBar>控件的<xref:System.Windows.Forms.ProgressBar.Minimum%2A>和<xref:System.Windows.Forms.ProgressBar.Maximum%2A>值。  
  
2.  在代码中，设置控件的<xref:System.Windows.Forms.ProgressBar.Value%2A>属性设置为已建立的最小值和最大值之间的整数值。  
  
    > [!NOTE]
    >  如果您设置<xref:System.Windows.Forms.ProgressBar.Value%2A>属性来建立边界之外<xref:System.Windows.Forms.ProgressBar.Minimum%2A>并<xref:System.Windows.Forms.ProgressBar.Maximum%2A>属性，该控件将引发<xref:System.ArgumentException>异常。  
  
     下面的代码示例演示了如何设置<xref:System.Windows.Forms.ProgressBar>直接值。 该代码从数据源中读取记录并更新进度条和标签，每次读取的数据记录。 此示例要求你的窗体具有<xref:System.Windows.Forms.Label>控件，<xref:System.Windows.Forms.ProgressBar>控件，并带有名为的行的数据表`CustomerRow`与`FirstName`和`LastName`字段。  
  
    ```vb  
    Public Sub CreateNewRecords()  
       ' Sets the progress bar's Maximum property to  
       ' the total number of records to be created.  
       ProgressBar1.Maximum = 20  
  
       ' Creates a new record in the dataset.  
       ' NOTE: The code below will not compile, it merely  
       ' illustrates how the progress bar would be used.  
       Dim anyRow As CustomerRow = DatasetName.ExistingTable.NewRow  
       anyRow.FirstName = "Stephen"  
       anyRow.LastName = "James"  
       ExistingTable.Rows.Add(anyRow)  
  
       ' Increases the value displayed by the progress bar.  
       ProgressBar1.Value += 1  
       ' Updates the label to show that a record was read.  
       Label1.Text = "Records Read = " & ProgressBar1.Value.ToString()  
    End Sub  
    ```  
  
    ```csharp  
    public void createNewRecords()  
    {  
       // Sets the progress bar's Maximum property to  
       // the total number of records to be created.  
       progressBar1.Maximum = 20;  
  
       // Creates a new record in the dataset.  
       // NOTE: The code below will not compile, it merely  
       // illustrates how the progress bar would be used.  
       CustomerRow anyRow = DatasetName.ExistingTable.NewRow();  
       anyRow.FirstName = "Stephen";  
       anyRow.LastName = "James";  
       ExistingTable.Rows.Add(anyRow);  
  
       // Increases the value displayed by the progress bar.  
       progressBar1.Value += 1;  
       // Updates the label to show that a record was read.  
       label1.Text = "Records Read = " + progressBar1.Value.ToString();  
    }  
    ```  
  
     如果要显示将继续按固定间隔的进度，您可以设置的值，然后调用方法，使<xref:System.Windows.Forms.ProgressBar>由该时间间隔内的控件的值。 这可用于计时器和其他不在此测量进度为占总体的方案。  
  
### <a name="to-increase-the-progress-bar-by-a-fixed-value"></a>若要按固定值增加进度栏  
  
1.  设置<xref:System.Windows.Forms.ProgressBar>控件的<xref:System.Windows.Forms.ProgressBar.Minimum%2A>和<xref:System.Windows.Forms.ProgressBar.Maximum%2A>值。  
  
2.  设置控件的<xref:System.Windows.Forms.ProgressBar.Step%2A>属性设置为一个整数，表示数量增加进度栏显示值。  
  
3.  调用<xref:System.Windows.Forms.ProgressBar.PerformStep%2A>方法，以更改所显示的设置的金额值<xref:System.Windows.Forms.ProgressBar.Step%2A>属性。  
  
     下面的代码示例演示了一个进度栏如何维护复制操作中的文件数。  
  
     在以下示例中，每个文件读取到内存中，进度栏，标签会相应地更新，以反映读取的文件总数。 此示例要求你的窗体具有<xref:System.Windows.Forms.Label>控件和一个<xref:System.Windows.Forms.ProgressBar>控件。  
  
    ```vb  
    Public Sub LoadFiles()  
       ' Sets the progress bar's minimum value to a number representing  
       ' no operations complete -- in this case, no files read.  
       ProgressBar1.Minimum = 0  
       ' Sets the progress bar's maximum value to a number representing  
       ' all operations complete -- in this case, all five files read.  
       ProgressBar1.Maximum = 5  
       ' Sets the Step property to amount to increase with each iteration.  
       ' In this case, it will increase by one with every file read.  
       ProgressBar1.Step = 1  
  
       ' Dimensions a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be copied into memory,  
       ' so the loop will execute 5 times.  
       For i = 0 To 4  
          ' Insert code to copy a file  
          ProgressBar1.PerformStep()  
          ' Update the label to show that a file was read.  
          Label1.Text = "# of Files Read = " & ProgressBar1.Value.ToString  
       Next i  
    End Sub  
    ```  
  
    ```csharp  
    public void loadFiles()  
    {  
       // Sets the progress bar's minimum value to a number representing  
       // no operations complete -- in this case, no files read.  
       progressBar1.Minimum = 0;  
       // Sets the progress bar's maximum value to a number representing  
       // all operations complete -- in this case, all five files read.  
       progressBar1.Maximum = 5;  
       // Sets the Step property to amount to increase with each iteration.  
       // In this case, it will increase by one with every file read.  
       progressBar1.Step = 1;  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be copied into memory,  
       // so the loop will execute 5 times.  
       for (int i = 0; i <= 4; i++)  
       {  
          // Inserts code to copy a file  
          progressBar1.PerformStep();  
          // Updates the label to show that a file was read.  
          label1.Text = "# of Files Read = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
     最后，您可以增加显示一个进度栏，以便每一项增加数量都是唯一的值。 这很有用，当你所跟踪的一系列唯一的操作，如不同大小的文件写入硬盘，或作为整体的百分比测量进度。  
  
### <a name="to-increase-the-progress-bar-by-a-dynamic-value"></a>若要通过动态值增加进度栏  
  
1.  设置<xref:System.Windows.Forms.ProgressBar>控件的<xref:System.Windows.Forms.ProgressBar.Minimum%2A>和<xref:System.Windows.Forms.ProgressBar.Maximum%2A>值。  
  
2.  调用<xref:System.Windows.Forms.ProgressBar.Increment%2A>方法，以更改显示你指定一个整数的值。  
  
     下面的代码示例演示了一个进度栏可以计算复制操作期间已使用多少磁盘空间。  
  
     在以下示例中，每个文件写入到硬盘，进度栏，标签会相应地更新，以反映可用硬盘空间量。 此示例要求你的窗体具有<xref:System.Windows.Forms.Label>控件和一个<xref:System.Windows.Forms.ProgressBar>控件。  
  
    ```vb  
    Public Sub ReadFiles()  
       ' Sets the progress bar's minimum value to a number   
       ' representing the hard disk space before the files are read in.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example and  
       ' will not compile.  
       ProgressBar1.Minimum = AvailableDiskSpace()  
       ' Sets the progress bar's maximum value to a number   
       ' representing the total hard disk space.  
       ' You will most likely have to set this using a system call.  
       ' NOTE: The code below is meant to be an example   
       ' and will not compile.  
       ProgressBar1.Maximum = TotalDiskSpace()  
  
       ' Dimension a counter variable.  
       Dim i As Integer  
       ' Uses a For...Next loop to iterate through the operations to be  
       ' completed. In this case, five files are to be written to the disk,  
       ' so it will execute the loop 5 times.  
       For i = 1 To 5  
          ' Insert code to read a file into memory and update file size.  
          ' Increases the progress bar's value based on the size of   
          ' the file currently being written.  
          ProgressBar1.Increment(FileSize)  
          ' Updates the label to show available drive space.  
          Label1.Text = "Current Disk Space Used = " &_   
          ProgressBar1.Value.ToString()  
       Next i  
    End Sub  
    ```  
  
    ```csharp  
    public void readFiles()  
    {  
       // Sets the progress bar's minimum value to a number   
       // representing the hard disk space before the files are read in.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example and   
       // will not compile.  
       progressBar1.Minimum = AvailableDiskSpace();  
       // Sets the progress bar's maximum value to a number   
       // representing the total hard disk space.  
       // You will most likely have to set this using a system call.  
       // NOTE: The code below is meant to be an example   
       // and will not compile.  
       progressBar1.Maximum = TotalDiskSpace();  
  
       // Uses a for loop to iterate through the operations to be  
       // completed. In this case, five files are to be written  
       // to the disk, so it will execute the loop 5 times.  
       for (int i = 1; i<= 5; i++)  
       {  
          // Insert code to read a file into memory and update file size.  
          // Increases the progress bar's value based on the size of   
          // the file currently being written.  
          progressBar1.Increment(FileSize);  
          // Updates the label to show available drive space.  
          label1.Text = "Current Disk Space Used = " + progressBar1.Value.ToString();  
       }  
    }  
    ```  
  
## <a name="see-also"></a>请参阅
- <xref:System.Windows.Forms.ProgressBar>
- <xref:System.Windows.Forms.ToolStripProgressBar>
- [ProgressBar 控件概述](progressbar-control-overview-windows-forms.md)
- [ProgressBar 控件](progressbar-control-windows-forms.md)
