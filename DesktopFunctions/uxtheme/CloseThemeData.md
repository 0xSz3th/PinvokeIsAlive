
## C# Signature:
```cs
[DllImport("uxtheme.dll", ExactSpelling=true)]
public extern static Int32 CloseThemeData(IntPtr hTheme);
```

## VB .NET Signature:
```cs
Declare Function CloseThemeData Lib "uxtheme.dll" (ByVal hTheme As IntPtr) As Int32

<DllImport("UxTheme.dll", CallingConvention:=CallingConvention.Cdecl)> _
Function CloseThemeData(ByVal hTheme As IntPtr) As Int32
End Function
```
