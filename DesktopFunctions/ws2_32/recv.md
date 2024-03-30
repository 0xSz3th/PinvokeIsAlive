
## C# Signature:       
```cs
[DllImport("ws2_32.dll")]
    public static extern int recvfrom(IntPtr Socket, IntPtr buf, int len, SendDataFlags flags, ref SockAddr from, IntPtr fromlen);

    public static int recvfrom(IntPtr Socket, IntPtr buf, int len, SendDataFlags flags, ref SockAddr from)
    {
        return recvfrom(Socket, buf, len, flags, ref from, IntPtr.Zero);
    }
```

## VB Signature:
```cs
Declare Function RecvFrom Lib "ws2_32.dll" (TODO) As TODO
```
