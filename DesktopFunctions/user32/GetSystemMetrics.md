
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int GetSystemMetrics(SystemMetric smIndex);
```

## VB.NET Signature:
```cs
Public Declare Auto Function GetSystemMetrics Lib "user32.dll" (ByVal smIndex As Integer) As Integer
```

## Sample Code C#:
```cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;
namespace CodeCoreUI_Diagnostics
{
     public partial class Form1:Form
     {
     public partial class WindowsAPI
     {
  //         *** PASTE SYSTEMMETRIC ENUM HERE *** 
          [DllImport("user32.dll")]
          public static extern int GetSystemMetrics(SystemMetric smIndex);
      }

     public Form1()
     {
         InitializeComponent();
     }

     private void Form1_Load(object sender,EventArgs e)
     {        
         ListView lvMain = new ListView();
         this.Controls.Add(lvMain);

         lvMain.Visible=true;
         lvMain.Location=new Point(0,0);
         lvMain.Dock = DockStyle.Fill;
         lvMain.Columns.Add("Name",200);
         lvMain.Columns.Add("Value",200) ;
         lvMain.Columns.Add("Returned",200);

         lvMain.View=View.Details;


         ListViewItem lvi;
         string x;
         int u;

         foreach (int i in Enum.GetValues(typeof(WindowsAPI.SystemMetric)))
         {
         x = Enum.GetName(typeof(WindowsAPI.SystemMetric),i);
         u=WindowsAPI.GetSystemMetrics(( WindowsAPI.SystemMetric)i);
         lvi = lvMain.Items.Add(x);        
         lvi.SubItems.Add(i.ToString());
         lvi.SubItems.Add(u.ToString()); 
         }
     }
     }
}
```
