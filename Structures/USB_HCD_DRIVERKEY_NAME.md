
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct USB_HCD_DRIVERKEY_NAME
{
   public int ActualLength;
   [MarshalAs(UnmanagedType.ByValTStr, SizeConst = BUFFER_SIZE)]
   public string DriverKeyName;
}
```

## VB Definition:
```cs
Structure USB_HCD_DRIVERKEY_NAME 
   Public TODO
End Structure
```

## Notes:
```cs
typedef struct _USB_HCD_DRIVERKEY_NAME {
   ULONG ActualLength;
   WCHAR DriverKeyName[1];
} USB_HCD_DRIVERKEY_NAME, *PUSB_HCD_DRIVERKEY_NAME;
```
