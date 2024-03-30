
## C# Signature:
```cs
[DllImport("uxtheme", ExactSpelling=true)]
public extern static Int32 GetThemePropertyOrigin(IntPtr hTheme, int iPartId, int iStateId, int iPropId, out PropertyOrigin pOrigin);
```

## VB .NET Signature:
```cs
Declare Function GetThemePropertyOrigin Lib "uxtheme.dll" (TODO) As TODO

<DllImport("uxtheme", ExactSpelling := True)> _
Public Shared Function GetThemePropertyOrigin(hTheme As IntPtr, iPartId As Integer, iStateId As Integer, iPropId As Integer, ByRef pOrigin As PropertyOrigin) As Int32
End Function
```
