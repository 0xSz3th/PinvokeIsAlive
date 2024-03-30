
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct INSTALLERINFO
{
    [MarshalAs(UnmanagedType.LPTStr)] public string pApplicationId;
    [MarshalAs(UnmanagedType.LPTStr)] public string pDisplayName;
    [MarshalAs(UnmanagedType.LPTStr)] public string pProductName;
    [MarshalAs(UnmanagedType.LPTStr)] public string pMfgName;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Structure INSTALLERINFO
    Public pApplicationId As String
    Public pDisplayName As String
    Public pProductName As String
    Public pMfgName As String
End Structure
```
