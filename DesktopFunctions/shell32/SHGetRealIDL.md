
## C# Signature:
```cs
/// <summary>
/// SHGetRealIDL converts a simple PIDL to a full PIDL.
/// </summary>
/// <param name="psf">[in] Pointer to an instance of IShellFolder whose simple pointer to an item identifier list (PIDL) is to be converted.</param>
/// <param name="pidlSimple">[in] The simple PIDL to be converted.</param>
/// <param name="pidlReal">[out] Pointer to the full converted PIDL. If the function fails, this parameter is set to NULL.</param>
/// <returns>Returns S_OK if successful, or an error value otherwise. </returns>
[DllImport("shell32.dll")]
public static extern IntPtr SHGetRealIDL(
               IShellFolder        psf,
            IntPtr            pidlSimple,
            out IntPtr        pidlReal ) ;
```

## VB Signature:
```cs
Declare Function SHGetRealIDL Lib "shell32.dll" (TODO) As TODO
```
