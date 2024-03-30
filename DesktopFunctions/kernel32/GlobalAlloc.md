
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr GlobalAlloc(uint uFlags, UIntPtr dwBytes);
```

## VB.Net Signature:
```cs
<DllImport("kernel32.dll", ExactSpelling:=True)> _
    Friend Shared Function GlobalAlloc(ByVal flags As Integer, ByVal size As Integer) As IntPtr
    End Function
```

## VB.Net Signature:
```cs
<DllImport("KERNEL32.DLL", EntryPoint:="GlobalAlloc", _
       SetLastError:=True, CharSet:=CharSet.Unicode, _
       ExactSpelling:=True, _
       CallingConvention:=CallingConvention.StdCall)> _
    Public Shared Function GlobalAlloc(ByVal src As Long, ByVal dst As Long) As Integer
    ' Leave function empty!
    End Function
```
