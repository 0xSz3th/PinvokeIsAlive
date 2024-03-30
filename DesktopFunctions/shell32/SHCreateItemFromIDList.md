
## C# Signature:
```cs
[DllImport("shell32.dll", PreserveSig = false)]
public static extern void SHCreateItemFromIDList(
    [In] IntPtr pidl,
    [In, MarshalAs(UnmanagedType.LPStruct)] Guid riid,
    [Out, MarshalAs(UnmanagedType.Interface, IidParameterIndex = 2)] out IShellItem ppv);
```

## VB Signature:
```cs
Declare Function SHCreateItemFromIDList Lib "shell32.dll" (TODO) As TODO
```
