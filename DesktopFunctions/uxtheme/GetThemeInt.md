
## C# Signature:
```cs
[DllImport("uxtheme", ExactSpelling=true)]
public extern static Int32 GetThemeIntList(IntPtr hTheme, int iPartId, int iStateId, int iPropId, out INTLIST pIntList);
```

## VB .NET Signature:
```cs
Declare Function GetThemeIntList Lib "uxtheme.dll" (TODO) As TODO

<DllImport("uxtheme", ExactSpelling := True)> _
Public Shared Function GetThemeIntList(hTheme As IntPtr, iPartId As Integer, iStateId As Integer, iPropId As Integer, ByRef pIntList As INTLIST) As Int32
End Function
```
