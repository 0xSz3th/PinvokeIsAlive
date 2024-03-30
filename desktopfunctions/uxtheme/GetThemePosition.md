
## C# Signature:
```cs
[DllImport("uxtheme", ExactSpelling=true)]
public extern static Int32 GetThemePosition(IntPtr hTheme, int iPartId, int iStateId, int iPropId, out POINT pPoint);
```

## VB .NET Signature:
```cs
Declare Function GetThemePosition Lib "uxtheme.dll" (TODO) As TODO

<DllImport("uxtheme", ExactSpelling := True)> _
Public Shared Function GetThemePosition(hTheme As IntPtr, iPartId As Integer, iStateId As Integer, iPropId As Integer, ByRef pPoint As POINT) As Int32
End Function
```
