
## C# Signature:
```cs
[DllImport("UxTheme.Dll", EntryPoint = "#2", CharSet = CharSet.Unicode)]
public static extern int OpenThemeFile(string pszFilename, string pszColor, string pszSize, out IntPtr hThemeFile, int dwReserved);
```

## VB Signature:
```cs
<DllImport("UxTheme.DLL", BestFitMapping:=False, CallingConvention:=CallingConvention.Winapi, CharSet:=CharSet.Unicode, EntryPoint:="#2")> _
Declare Function OpenThemeFile Lib "uxtheme.dll" (ByVal String pszFilename, ByVal String pszColor, ByVal String pszSize, ByRef IntPtr hThemeFile, ByVal Integer dwReserved) As Integer

<DllImport("UxTheme.Dll", EntryPoint := "#2", CharSet := CharSet.Unicode)> _
Public Shared Function OpenThemeFile(pszFilename As String, pszColor As String, pszSize As String, ByRef hThemeFile As IntPtr, dwReserved As Integer) As Integer
End Function
```

## Pascal/Delphi Signature:
```cs
Function OpenThemeFile(pszThemeFileName: LPCWSTR; pszColorName: LPCWSTR; pszSizeName: LPCWSTR; hThemeFile: Pointer; unknown: DWORD): HRESULT; StdCall; External 'uxtheme.dll' Index 2;
```
