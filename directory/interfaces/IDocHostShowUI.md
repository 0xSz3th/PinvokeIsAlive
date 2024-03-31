
## C# Definition:
```cs
[ComImport]
[Guid("C4D244B0-D43E-11CF-893B-00AA00BDCE1A")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown) ]
public interface IDocHostShowUI
{
     [PreserveSig]
     uint ShowMessage(IntPtr hwnd, 
     [MarshalAs(UnmanagedType.LPWStr)] string lpstrText, 
     [MarshalAs(UnmanagedType.LPWStr)] string lpstrCaption, 
     uint dwType, 
     [MarshalAs(UnmanagedType.LPWStr)] string lpstrHelpFile, 
     uint dwHelpContext,
     out int lpResult);

     [PreserveSig]
     uint ShowHelp(IntPtr hwnd, [MarshalAs(UnmanagedType.LPWStr)] string pszHelpFile, 
     uint uCommand, uint dwData, 
     tagPOINT ptMouse, 
     [MarshalAs(UnmanagedType.IDispatch)] object pDispatchObjectHit);               
}
```

## VB Definition:
```cs
<ComImport(), Guid("C4D244B0-D43E-11CF-893B-00AA00BDCE1A"), InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
  Public Interface         
    <PreserveSig()> _
    Function ShowMessage(ByVal hwnd As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> ByVal lpstrText As String, <MarshalAs(UnmanagedType.LPWStr)> ByVal lpstrCaption As String, ByVal dwType As Integer, <MarshalAs(UnmanagedType.LPWStr)> ByVal lpstrHelpFile As String, ByVal dwHelpContext As Integer, ByRef lpResult As Integer) As Integer

    <PreserveSig()> _
    Function ShowHelp(ByVal hwnd As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> ByVal pszHelpFile As String, ByVal uCommand As Integer, ByVal dwData As Integer, ByVal ptMouse As tagPoint, <MarshalAs(UnmanagedType.IDispatch)> ByVal pDispatchObjectHit As Object) As Integer
End Interface
```
