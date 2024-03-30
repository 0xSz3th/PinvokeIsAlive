
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern int GetTimeFormat(uint locale, uint dwFlags, ref SystemTime time, string format, StringBuilder sb, int sbSize);
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    private struct SystemTime {
        [MarshalAs(UnmanagedType.U2)] public ushort Year;
        [MarshalAs(UnmanagedType.U2)] public ushort Month;
        [MarshalAs(UnmanagedType.U2)] public ushort DayOfWeek;
        [MarshalAs(UnmanagedType.U2)] public ushort Day;
        [MarshalAs(UnmanagedType.U2)] public ushort Hour;
        [MarshalAs(UnmanagedType.U2)] public ushort Minute;
        [MarshalAs(UnmanagedType.U2)] public ushort Second;
        [MarshalAs(UnmanagedType.U2)] public ushort Milliseconds;
    }
```

## Alternative Managed API:
```cs
DateTime.ToString(string format, IFormatProvider provider);
```
