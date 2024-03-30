
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern uint GetWindowsDirectory(StringBuilder lpBuffer,
   uint uSize);
```

## VB.NET Signature
```cs
<DllImport("kernel32.dll", SetLastError:=true, EntryPoint:="GetWindowsDirectoryW", CharSet:=CharSet.Unicode)> _
Public Function GetWindowsDirectory(<MarshalAs(UnmanagedType.LPTSTR)>lpBuffer As System.Text.StringBuilder, _
                   uSize As UInteger ) As UInteger
End function
```

## VB Signature
```cs
Declare Function GetWindowsDirectory Lib "kernel32" Alias "GetWindowsDirectoryA" _
   (ByVal Buffer As String, ByVal Size As Integer) As Integer
```

## Tips & Tricks:
```cs
Private Sub test()
      Dim sSystemPath As String = System.Environment.GetFolderPath(Environment.SpecialFolder.System)
      MessageBox.Show(sSystemPath.Substring(0, sSystemPath.LastIndexOf("\")))
      MessageBox.Show(System.Environment.GetEnvironmentVariable("windir"))
   End Sub
```

## VB Sample Code:
```cs
As SDim WinDir tring = Space(255)
   Dim Res As Integer = GetWindowsDirectory(WinDir, WinDir.Length)
   WinDir = WinDir.Substring(0, Res)
```

## VB.NET Sample Code:
```cs
Shared Function wins() As String
     Dim sb As StringBuilder =new StringBuilder(100)
     Dim f as UInteger = 100
     GetWindowsDirectory(sb,i)
     return sb.ToString()  
End Function
```

## C# Sample Code:
```cs
const int MaxPathLength = 255;
   StringBuilder sb = new StringBuilder(MaxPathLength);
   int len = (int)GetWindowsDirectory(sb, MaxPathLength);
   _windowsDirectory = sb.ToString(0, len);
```

## C# Sample Code (Alternative):
```cs
static string wins()
{
     StringBuilder sb =new StringBuilder(100);
     int i = 100; uint f;
     GetWindowsDirectory(sb,ref  i);
     return sb.ToString()  ;
}
```
