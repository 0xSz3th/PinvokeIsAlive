
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet = CharSet.Unicode, PreserveSig = false)]
public static extern void SHCreateItemWithParent(
    [In] IntPtr pidlParent,
    [In] IShellFolder psfParent, 
    [In] IntPtr pidl,
    [In, MarshalAs(UnmanagedType.LPStruct)] Guid riid,
    [Out, MarshalAs(UnmanagedType.Interface, IidParameterIndex = 3)] out IShellItem ppv);
```

## VB Signature:
```cs
Declare Function SHCreateItemWithParent Lib "shell32.dll" (TODO) As TODO
```
