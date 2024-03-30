
## C# Signature:
```cs
[ComImport,
    Guid("ea1afb91-9e28-4b86-90e9-9e9f8a5eefaf"),
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface ITaskbarList2 : ITaskbarList
    {
    /// <summary>
    /// Marks a window as full-screen
    /// </summary>
    /// <param name="hWnd"></param>
    /// <param name="fFullscreen"></param>
    void MarkFullscreenWindow([In] IntPtr hWnd, [In] int fFullscreen);
    }
```

## VB Signature:
```cs
Declare Function ITaskbarList2 Lib "shell32.dll" (TODO) As TODO
```
