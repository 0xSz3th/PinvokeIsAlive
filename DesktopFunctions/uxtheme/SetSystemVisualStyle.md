
## C# Signature:
```cs
[DllImport("UxTheme.Dll", EntryPoint = "#65", CharSet = CharSet.Unicode)]
public static extern int SetSystemVisualStyle(string pszFilename, string pszColor, string pszSize, int dwReserved);
```

## VB Signature:
```cs
<DllImport("UxTheme.DLL", BestFitMapping:=False, CallingConvention:=CallingConvention.Winapi, CharSet:=CharSet.Unicode, EntryPoint:="#65")> _
Shared Function SetSystemVisualStyle(ByVal pszFilename As String, ByVal pszColor As String, ByVal pszSize As String, ByVal dwReserved As Integer) As Integer
End Function
```

## Usage:
```cs
pszFilename
```

## Usage:
```cs
pszColor
```

## Usage:
```cs
pszSize
```

## Sample Code C#:
```cs
// This will set your Visual Style to Luna
SetSystemVisualStyle(@"C:\WINDOWS\resources\Themes\Luna\Luna.msstyles", "Metallic", "NormalSize", 0);
```

## Sample Code VB.NET:
```cs
SetSystemVisualStyle("C:\WINDOWS\resources\Themes\Luna\Luna.msstyles", "Metallic", "NormalSize", 0)
```
