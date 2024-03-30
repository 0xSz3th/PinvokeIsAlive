
## C# Signatures:
```cs
// When calling with any variable parameters and Ansi
[DllImport("msvcrt.dll", CharSet = CharSet.Ansi,
    CallingConvention = CallingConvention.Cdecl)]
static extern int sprintf(
    StringBuilder buffer,
    string format,
    __arglist);

// When calling with any variable parameters and Unicode
[DllImport("msvcrt.dll", CharSet = CharSet.Unicode,
    CallingConvention = CallingConvention.Cdecl)]
static extern int swprintf(
    StringBuilder buffer,
    string format,
    __arglist);

// When calling with 1 arg
[DllImport("msvcrt.Dll", CallingConvention=CallingConvention.Cdecl)]
static extern int sprintf([In,Out]StringBuilder buffer, String fmt, 
    String arg1);

// When calling with 2 args
[DllImport("msvcrt.Dll", CallingConvention=CallingConvention.Cdecl)]
static extern int sprintf([In,Out]StringBuilder buffer, String fmt, 
    String arg1, String arg2);

// When calling with 3 args
[DllImport("msvcrt.Dll", CallingConvention=CallingConvention.Cdecl)]
static extern int sprintf([In,Out]StringBuilder buffer, String fmt, 
    String arg1, String arg2, String arg3);
```

## VB Signature:
```cs
<DllImport("msvcrt.dll", CharSet:=CharSet.Ansi, 
  CallingConvention:=CallingConvention.Cdecl, 
  ExactSpelling:=True)> _
  Public Shared Function sprintf(ByVal TargetString As System.Text.StringBuilder, 
    ByVal  FormatSpecifier As String, ByVal i As Int32) As Int32
  End Function
```
