
## C# Signature:
```cs
[DllImport("Ws2_32.dll")]
    public static extern int connect(IntPtr s, ref sockaddr_in addr, int addrsize);

    [DllImport("Ws2_32.dll")]
    public static extern int connect(IntPtr s, ref sockaddr_in6 addr, int addrsize);
```

## VB Signature:
```cs
Declare Function connect Lib "ws2_32.dll" (TODO) As TODO
```
