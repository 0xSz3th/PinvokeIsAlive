
## C# Definition:
```cs
[StructLayout ( LayoutKind.Sequential, CharSet = CharSet.Auto, Pack = 4 )]
struct COMDLG_FILTERSPEC
{
    [MarshalAs ( UnmanagedType.LPWStr )]
    public string pszName;

    [MarshalAs ( UnmanagedType.LPWStr )]
    public string pszSpec;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto, Pack:=4)>
    Structure COMDLG_FILTERSPEC

    <MarshalAs(UnmanagedType.LPWStr)>
    Public pszName As String

    <MarshalAs(UnmanagedType.LPWStr)>
    Public pszSpec As String
    End Structure
```
