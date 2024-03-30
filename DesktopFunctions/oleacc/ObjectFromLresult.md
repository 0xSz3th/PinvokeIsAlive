
## C# Signature:
```cs
[DllImport("oleacc.dll", PreserveSig=false)]
[return: MarshalAs(UnmanagedType.Interface)]
static extern object ObjectFromLresult(UIntPtr lResult, 
     [MarshalAs(UnmanagedType.LPStruct)] Guid refiid, IntPtr wParam);
```

## VB Signature:
```cs
Declare Auto Function ObjectFromLresult Lib "oleacc.dll" (ByVal lResult As UIntPtr, <MarshalAs(UnmanagedType.LPStruct)> ByVal refiid As Guid, ByVal wParam As IntPtr) As <MarshalAs(UnmanagedType.Interface)> Object
```

## VB Signature:
```cs
<Dllimport("oleacc.dll")> _
Shared Function ObjectFromLresult(ByVal lResult As UIntPtr, <MarshalAs(UnmanagedType.LPStruct)> ByVal refiid As Guid, ByVal wParam As IntPtr) As <MarshalAs(UnmanagedType.Interface)> Object
End Function
```

## Sample Code:
```cs
// Get the ActiveX interface of some window of class "Internet Explorer_Server"
IntPtr hWnd = GetThatWindow(); // from wherever
uint nMsg = RegisterWindowMessage("WM_HTML_GETOBJECT");
UIntPtr lRes;
if ( SendMessageTimeout(hWnd, nMsg, UIntPtr.Zero, IntPtr.Zero, 
     SendMessageTimeoutFlags.SMTO_ABORTIFHUNG, 1000, out lRes) == IntPtr.Zero )
     return null;
return (mshtml.IHTMLDocument) ObjectFromLresult(lRes, 
     typeof(mshtml.IHTMLDocument).GUID, IntPtr.Zero);
```
