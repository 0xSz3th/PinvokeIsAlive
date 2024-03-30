
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct FILETIME {
    public uint DateTimeLow;
    public uint DateTimeHigh;
}
```

## VB.Net Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure FILETIME
   Public dwLowDateTime As UInteger
   Public dwHighDateTime As UInteger

   Public ReadOnly Property Value() As ULong
     Get
       Return CType(dwHighDateTime << 32, ULong) + dwLowDateTime
     End Get
   End Property
End Structure
```

## Sample Code:
```cs
public static DateTime FiletimeToDateTime(FILETIME fileTime) {
        long hFT2 = (((long) fileTime.dwHighDateTime) << 32) | ((uint) fileTime.dwLowDateTime);
        return DateTime.FromFileTimeUtc(hFT2);
    }

    public static FILETIME DateTimeToFiletime(DateTime time) {
        FILETIME ft;
        long hFT1 = time.ToFileTimeUtc();
        ft.dwLowDateTime = (int) (hFT1 & 0xFFFFFFFF);
        ft.dwHighDateTime = (int) (hFT1 >> 32);
        return ft;
    }
```

## Sample Code:
```cs
Private Shared Function ConvertFileTimeToDateTime(input As FILETIME) As DateTime
    Dim longTime As ULong = (CType(input.dwHighDateTime, ULong) << 32) Or input.dwLowDateTime
    Return DateTime.FromFileTime(longTime)
    End Function
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct FILETIME {
        private long timestamp;
        public DateTime Local { 
            get { return DateTime.FromFileTime(this.timestamp); }
            set { this.timestamp = value.ToFileTime(); }
        }
        public DateTime Utc { 
            get { return DateTime.FromFileTimeUtc(this.timestamp); }
            set { this.timestamp = value.ToFileTimeUtc(); }
        }
    }
```
