
## C# Signature:
```cs
[DllImport("kernel32.dll",
        CallingConvention=CallingConvention.Winapi, 
        SetLastError=true)]
static extern bool FileTimeToSystemTime([In] ref FILETIME lpFileTime,
   out SYSTEMTIME lpSystemTime);
```

## VB.Net Signature
```cs
<DllImport( _
       "kernel32.dll", _
       CharSet:=CharSet.Auto, _
       SetLastError:=True)> _
   Friend Shared Function FileTimeToSystemTime( _
                        <[In]()> ByRef lpFileTime As FILETIME, _
                        <Out()> ByRef lpSystemTime As SYSTEMTIME) _
               As Boolean
   End Function
```

## Sample Code:
```cs
public static DateTime FileTimeToSystemTime(string hexTS) {
        string lowDT = string.Format("{0}{1}{2}{3}",
            hexTS.Substring(6, 2), hexTS.Substring(4, 2), hexTS.Substring(2, 2), hexTS.Substring(0, 2));

        string highDT = string.Format("{0}{1}{2}{3}",
            hexTS.Substring(14, 2), hexTS.Substring(12, 2), hexTS.Substring(10, 2), hexTS.Substring(8, 2));

        FILETIME fileTime;
        fileTime.dwHighDateTime = int.Parse(highDT, System.Globalization.NumberStyles.HexNumber);
        fileTime.dwLowDateTime = int.Parse(lowDT, System.Globalization.NumberStyles.HexNumber);
        long hFT2 = (((long)fileTime.dwHighDateTime) << 32) | ((uint)fileTime.dwLowDateTime);
        return DateTime.FromFileTimeUtc(hFT2);
    }
```
