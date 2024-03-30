
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool SetWindowDisplayAffinity(IntPtr hwnd, DisplayAffinity affinity);
```

## VB Signature:
```cs
Declare Function SetWindowDisplayAffinity Lib "user32.dll" (hwnd As IntPtr, affinity As DisplayAffinity) As Boolean
```

## User-Defined Types:
```cs
enum DisplayAffinity : uint
{
   None = 0x00,
   Monitor = 0x01,
   ExcludeFromCapture = 0x11
}
```
