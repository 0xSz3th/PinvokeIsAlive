
## C# Signature:
```cs
using HANDLE = System.IntPtr;
using DWORD = System.UInt32;

[DllImport("netapi32.dll", SetLastError=true)]
internal static extern DWORD DsGetDcNext(
     HANDLE GetDcContextHandle,
     IntPtr SockAddressCount,
     IntPtr SockAddresses, //must free this if using (SocketAddressCount > 1)
     out IntPtr DnsHostName //will have to marshal this one manually
     );
```

## VB Signature:
```cs
Declare Function DsGetDcNext Lib "netapi32.dll" (TODO) As TODO
```
