
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct WINHTTP_CURRENT_USER_IE_PROXY_CONFIG
{
    [MarshalAs(UnmanagedType.Bool)]   bool   AutoDetect;
     [MarshalAs(UnmanagedType.LPWStr)] string AutoConfigUrl;
     [MarshalAs(UnmanagedType.LPWStr)] string Proxy;
     [MarshalAs(UnmanagedType.LPWStr)] string ProxyBypass;

}
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure WINHTTP_CURRENT_USER_IE_PROXY_CONFIG
     <MarshalAs(UnmanagedType.Bool)> _
     Dim AutoDetect As Boolean

     <MarshalAs(UnmanagedType.LPWStr)> _
     Dim AutoConfigUrl As String

     <MarshalAs(UnmanagedType.LPWStr)> _
     Dim Proxy As String

     <MarshalAs(UnmanagedType.LPWStr)> _
     Dim ProxyBypass As String
End Structure
```
