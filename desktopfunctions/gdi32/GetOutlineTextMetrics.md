
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern uint GetOutlineTextMetrics(IntPtr hdc, uint cbData, IntPtr ptrZero);
```

## Sample Code:
```cs
private static void GetOutlineMetrics(IntPtr hdc)
{
    uint cbBuffer = GetOutlineTextMetrics(hdc, 0, IntPtr.Zero);
    if (cbBuffer == 0)
        return;
    IntPtr buffer = Marshal.AllocHGlobal((int)cbBuffer);
      try
    {
        if (GetOutlineTextMetrics(hdc, cbBuffer, buffer) != 0)
        {
            OUTLINETEXTMETRIC otm = new OUTLINETEXTMETRIC();
            otm = (OUTLINETEXTMETRIC)Marshal.PtrToStructure(buffer, typeof(OUTLINETEXTMETRIC));
            string otmpFamilyName = Marshal.PtrToStringAnsi(new IntPtr((int)buffer + otm.otmpFamilyName));
            string otmpFaceName = Marshal.PtrToStringAnsi(new IntPtr((int)buffer + otm.otmpFaceName));;
            string otmpStyleName = Marshal.PtrToStringAnsi(new IntPtr((int)buffer + otm.otmpStyleName));;
            string otmpFullName = Marshal.PtrToStringAnsi(new IntPtr((int)buffer + otm.otmpFullName));;
        }
    }
    finally
    {
        Marshal.FreeHGlobal(buffer);
    }
}
```
