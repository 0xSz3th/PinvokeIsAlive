
## C# Signature:
```cs
[DllImport("shlwapi.dll", ExactSpelling=true, PreserveSig=false)]
public static extern Int32 SHAutoComplete(
    IntPtr hwndEdit,
    AutoCompleteFlags dwFlags
);
```

## VB .NET Signature:
```cs
Declare Function SHAutoComplete Lib "shlwapi.dll" (ByVal hWndEdit As IntPtr, ByVal dwFlags As AutoCompleteFlags) As Integer
```

## Sample Code:
```cs
Int32 res = SHAutoComplete(textBox1.Handle, AutoCompleteFlags.SHACF_FILESYSTEM);
```
