
## C# Signature:
```cs
[DllImport("winhttp.dll", SetLastError = true, CharSet = CharSet.Unicode)]
[return: MarshalAs(UnmanagedType.Bool)]
    public static extern Boolean WinHttpGetProxyForUrl(
        IntPtr hsession,
        [MarshalAs(UnmanagedType.LPWStr)] String lpcwszUrl,
        ref WINHTTP_AUTO_PROXY_OPTIONS pAutoProxyOptions,
        out WINHTTP_PROXY_INFO pProxyInfo);
```

## VB Signature:
```cs
Declare Function WinHttpGetProxyForUrl Lib "winhttp.dll" (TODO) As TODO
```
