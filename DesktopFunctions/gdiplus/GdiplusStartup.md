
## C# Signature:
```cs
[DllImport("gdiplus.dll", CharSet=CharSet.Unicode, ExactSpelling=true)]
static extern int GdiplusStartup(out IntPtr token, ref StartupInput input, 
out  StartupOutput output);
```

## VB Signature:
```cs
Declare Shared Function GdiplusStartup Lib "gdiplus.dll" (ByRef token As IntPtr, _
ByRef input As StartupInput, ByRef output As StartupOutput) As Integer
```

## VB Signature:
```cs
<DllImport("gdiplus.dll", EntryPoint:="GdiplusStartup", _
         SetLastError:=True, CharSet:=CharSet.Unicode, _
         ExactSpelling:=True, CallingConvention:=CallingConvention.StdCall)> _
Public Shared Function GdiplusStartup(ByRef token As IntPtr, _
                       ByRef input As GdipStartupInput, _
                       ByRef output As GdipStartupOutput) _
                       As Integer
End Function
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
struct StartupOutput
{
    public IntPtr hook;
    public IntPtr unhook;
}

[StructLayout(LayoutKind.Sequential)]
struct StartupInput
{
    public int GdiplusVersion = 1;
    public IntPtr DebugEventCallback;
    public bool SuppressBackgroundThread = false;
    public bool SuppressExternalCodecs = false;
}
```
