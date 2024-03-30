
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet = CharSet.Unicode, SetLastError = true)]
static extern int LCMapStringEx(
     string lpLocaleName,        //  LPCWSTR      lpLocaleName
     uint dwMapFlags,        //  DWORD        dwMapFlags
     string lpSrcStr,        //  LPCWSTR      lpSrcStr
     int cchSrc,             //  int          cchSrc
     [Out]
     IntPtr lpDestStr,           //  LPWSTR       lpDestStr
     int cchDest,            //  int          cchDest
     IntPtr lpVersionInformation,    //  LPNLSVERSIONINFO lpVersionInformation
     IntPtr lpReserved,          //  LPVOID       lpReserved
     IntPtr sortHandle);         //  LPARAM       sortHandle
```

## VB Signature:
```cs
Declare Function LCMapStringEx Lib "kernel32.dll" (TODO) As TODO
```

## Sample Code:
```cs
public static string ToLower(string src)
{
     string nResult = src;

     int nLen, nSize;

     uint dwMapFlags = LCMAP_LOWERCASE;
     IntPtr ptr, pZero = IntPtr.Zero;

     nLen = src.Length;
     nSize = LCMapStringEx(LOCALE_NAME_SYSTEM_DEFAULT, dwMapFlags, src, nLen, IntPtr.Zero, 0, pZero, pZero, pZero);
     if (nSize > 0)
     {
     nSize = nSize * sizeof(char);
     ptr = Marshal.AllocHGlobal(nSize);
     try
     {
         nSize = LCMapStringEx(LOCALE_NAME_SYSTEM_DEFAULT, dwMapFlags, src, nLen, ptr, nSize, pZero, pZero, pZero);
         if (nSize > 0) nResult = Marshal.PtrToStringUni(ptr, nSize);
     }
     finally
     {
         Marshal.FreeHGlobal(ptr);
     }
     }

     return nResult;
}
```
