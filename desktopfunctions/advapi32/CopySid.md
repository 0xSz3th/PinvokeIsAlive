
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError=true)]
static extern bool CopySid(uint nDestinationSidLength, IntPtr pDestinationSid,
   IntPtr pSourceSid);

[DllImport("advapi32.dll", SetLastError=true)]
static extern bool CopySid(uint nDestinationSidLength, byte[] pDestinationSid,
   IntPtr pSourceSid);
```

## VB Signature:
```cs
Declare Function CopySid Lib "advapi32.dll" (ByVal nDestinationSidLength As Integer, _
   ByVal pDestinationSid As IntPtr, ByVal pSourceSid As IntPtr) As Boolean
```

## Sample Code:
```cs
private static byte[] DuplicateSid(IntPtr pSid)
    {
        uint length = UnsafeNativeMethods.GetLengthSid(pSid);
        byte[] bytes = new byte[length];
        UnsafeNativeMethods.CopySid(length, bytes, pSid);
        return bytes;
    }
```
