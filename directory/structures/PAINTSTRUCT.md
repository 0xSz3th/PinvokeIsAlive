
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct PAINTSTRUCT {
   public IntPtr hdc;
   public bool fErase;
   public RECT rcPaint;
   public bool fRestore;
   public bool fIncUpdate;
   [MarshalAs(UnmanagedType.ByValArray, SizeConst=32)] public byte [] rgbReserved;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack := 4)> _
  Public Structure PAINTSTRUCT
    Public hdc As IntPtr
    Public fErase As Integer
    Public rcPaint As RECT
    Public fRestore As Integer
    Public fIncUpdate As Integer
    <MarshalAs(UnmanagedType.ByValArray, SizeConst := 32)> _
    Public rgbReserved As Byte()
End Structure
```
