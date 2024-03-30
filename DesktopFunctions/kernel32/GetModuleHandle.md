
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Unicode, SetLastError=true)]
public static extern IntPtr GetModuleHandle([MarshalAs(UnmanagedType.LPWStr)] string lpModuleName);
```

## VB.Net Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Unicode, SetLastError:=True)> _
Public Shared Function GetModuleHandle(<MarshalAs(UnmanagedType.LPWStr)> ByVal lpModuleName As String) As IntPtr
End Function
```

## Boo Signature:
```cs
[DllImport("kernel32", CharSet : CharSet.Auto)]
static def GetModuleHandle(lpModuleName as string) as IntPtr:
     pass
```

## Sample Code:
```cs
IntPtr handle = GetModuleHandle("user32.dll");
if (handle == IntPtr.Zero) {
    throw new Win32Exception(Marshal.GetLastWin32Error());
}
```
