
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet = CharSet.Unicode, PreserveSig = false)]
    public static extern void SHCreateItemFromParsingName(
        [In][MarshalAs(UnmanagedType.LPWStr)] string pszPath,
        [In] IntPtr pbc,
        [In][MarshalAs(UnmanagedType.LPStruct)] Guid riid,
        [Out][MarshalAs(UnmanagedType.Interface, IidParameterIndex = 2)] out IShellItem ppv);
```

## VB Signature:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Unicode, PreserveSig:=False)> _
     Public Shared Sub SHCreateItemFromParsingName( _
         <MarshalAs(UnmanagedType.LPWStr)> ByVal pszPath As String, _
         ByVal pbc As IntPtr, _
         <MarshalAs(UnmanagedType.LPStruct)> ByVal riid As Guid, _
         <MarshalAs(UnmanagedType.Interface, IidParameterIndex:=2)> ByRef ppv As IShellItem)
     End Sub
```

## Sample Code:
```cs
IShellItem oItem;
        SHCreateItemFromParsingName(path, IntPtr.Zero, typeof(IShellItem).GUID, out oItem);
```
