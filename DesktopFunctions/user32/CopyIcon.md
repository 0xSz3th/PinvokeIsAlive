
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr CopyIcon(IntPtr hIcon);
```

## VB Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function CopyIcon(ByVal hIcon As IntPtr) As IntPtr
End Function
```

## Notes:
```cs
static extern IntPtr LoadCursor(IntPtr hInstance, int lpCursorName);
```

## Sample Code:
```cs
private static string BusyCursorIcon { get; set; }
private static string DoneCursorIcon { get; set; }

private const uint OCR_NORMAL = 32512;
private const uint OCR_WAIT = 32514;

[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
private static extern IntPtr LoadCursorFromFile(string lpFileName);

[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
private static extern IntPtr CopyIcon(IntPtr hcur);

[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
private static extern bool SetSystemCursor(IntPtr hcur, uint id);

string folderPath = Path.GetDirectoryName(System.Reflection.Assembly.GetExecutingAssembly().Location);
BusyCursorIcon = Path.Combine(folderPath, "aero_busy_xl.ani");
DoneCursorIcon = Path.Combine(folderPath, "arrow_m.cur");

if (!File.Exists(BusyCursorIcon) || !File.Exists(DoneCursorIcon))
{
   // AB: use api only to change cursor; same call will switch cursor!
   SetSystemCursor(LoadCursor(IntPtr.Zero, OCR_WAIT), OCR_NORMAL);
}
else 
{
   IntPtr cursor = (working)  
    ? LoadCursorFromFile(BusyCursorIcon) 
    : LoadCursorFromFile(DoneCursorIcon);
   if (cursor != IntPtr.Zero)
     SetSystemCursor(CopyIcon(cursor), OCR_NORMAL);
   else
     SetSystemCursor(LoadCursor(IntPtr.Zero, OCR_WAIT), OCR_NORMAL);
}
```
