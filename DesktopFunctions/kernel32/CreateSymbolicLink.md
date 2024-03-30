
## C# Signature:
```cs
[DllImport("Kernel32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
[return: System.Runtime.InteropServices.MarshalAs(System.Runtime.InteropServices.UnmanagedType.I1)]
static extern bool CreateSymbolicLink(string lpSymlinkFileName, string lpTargetFileName, SYMBOLIC_LINK_FLAG dwFlags);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function CreateSymbolicLink(ByVal lpSymlinkFileName As String, ByVal lpTargetFileName As String, ByVal dwFlags As SYMBOLIC_LINK_FLAG) As Boolean
End Function
```

## Return Codes
```cs
new System.ComponentModel.Win32Exception()  // gets last WinAPI error, e.g., File Exists
```
