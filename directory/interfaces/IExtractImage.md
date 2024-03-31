
## C# Definition:
```cs
[ComImportAttribute()]
[GuidAttribute("BB2E617C-0920-11d1-9A0B-00C04FC2D6C1")]
[InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
interface IExtractImage
{
    void GetLocation(
        [Out, MarshalAs(UnmanagedType.LPWStr)]
        StringBuilder pszPathBuffer,
        int cch,
        ref int pdwPriority,
        ref SIZE prgSize,
        int dwRecClrDepth,
        ref int pdwFlags);

    void Extract(
        out IntPtr phBmpThumbnail);
}
```

## VB Definition:
```cs
''' <summary>
    ''' Exposes methods that request a thumbnail image from a Shell folder.
    ''' </summary>
    <ComImport()> _
    <Guid("BB2E617C-0920-11d1-9A0B-00C04FC2D6C1")> _
    <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
    <EditorBrowsable(EditorBrowsableState.Advanced)> _
    Friend Interface IExtractImage

    ''' <summary>
    ''' Gets a path to the image that is to be extracted.
    ''' </summary>
    ''' <returns>This method may return a COM-defined error code or one of the following: S_OK if successful, or E_PENDING.</returns>
    Function GetLocation( _
        <Out(), MarshalAs(UnmanagedType.LPWStr)> ByVal pszPathBuffer As System.Text.StringBuilder, _
        ByVal cch As Integer, _
        ByRef pdwPriority As Integer, _
        ByRef prgSize As Win32.SIZE, _
        ByVal dwRecClrDepth As Integer, _
        ByRef pdwFlags As Integer) As Integer

    ''' <summary>
    ''' Requests an image from an object, such as an item in a Shell folder.
    ''' </summary>
    ''' <returns>Returns S_OK if successful, or a COM-defined error code otherwise.</returns>
    Function Extract(<Out()> ByRef phBmpImage As IntPtr) As Integer

    End Interface
```

## User-Defined Types:
```cs
// You can use this enum for the IExtractImage.GetLocation method.
    [Flags]
    public enum IExtractImageFlags : int {
        Async = 0x1,
        Cache = 0x2,
        Aspect = 0x4,
        Offline = 0x8,
        Gleam = 0x10,
        Screen = 0x20,
        OriginalSize = 0x40,
        NoStamp = 0x80,
        NoBorder = 0x100,
        Quality = 0x200
    }
```
