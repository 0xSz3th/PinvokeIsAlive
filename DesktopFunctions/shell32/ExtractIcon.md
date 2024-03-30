
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern IntPtr ExtractIcon(IntPtr hInst, string lpszExeFileName, int nIconIndex);
```

## VB.NET Signature:
```cs
<DllImport("shell32.dll")> _
Private Shared Function ExtractIcon(ByVal hInst As IntPtr, ByVal lpszExeFileName As String, ByVal nIconIndex As Integer) As IntPtr
End Function
```

## C# Sample Code:
```cs
string fileName = "C:\\Test.txt";
IntPtr hIcon = ExtractIcon(IntPtr.Zero, filename, 0);
System.Drawing.Icon MyIcon = System.Drawing.Icon.FromHandle(hIcon);
pictureBox1.Image = MyIcon.ToBitmap();
```

## VB.NET Sample Code:
```cs
Dim fileName As String = "C:\Test.txt"
Dim hIcon As IntPtr =  ExtractIcon(IntPtr.Zero, filename, 0)
Dim MyIcon As System.Drawing.Icon = System.Drawing.Icon.FromHandle(hIcon)
pictureBox1.Image = MyIcon.ToBitmap()
```
