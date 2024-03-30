
## C# Signature:
```cs
/// <returns>If function succeeds, it returns 0(S_OK). Otherwise, it returns an error code.</returns>
    [DllImport("ole32.dll", CharSet = CharSet.Auto, SetLastError = true, CallingConvention = CallingConvention.StdCall)]
    public static extern int CoInitializeEx(
        [In, Optional] IntPtr pvReserved,
        [In]  COINIT dwCoInit //DWORD
        );
```

## Sample Code:
```cs
public enum COINIT : uint //tagCOINIT
    {
        COINIT_MULTITHREADED = 0x0, //Initializes the thread for multi-threaded object concurrency.
        COINIT_APARTMENTTHREADED = 0x2, //Initializes the thread for apartment-threaded object concurrency
        COINIT_DISABLE_OLE1DDE = 0x4, //Disables DDE for OLE1 support
        COINIT_SPEED_OVER_MEMORY = 0x8, //Trade memory for speed
    }
```
