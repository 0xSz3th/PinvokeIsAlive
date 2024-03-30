
## C# Signature:
```cs
/// <summary>
/// The URLMON library contains this function, URLDownloadToFile, which is a way
/// to download files without user prompts.  The ExecWB( _SAVEAS ) function always
/// prompts the user, even if _DONTPROMPTUSER parameter is specified, for "internet
/// security reasons".  This function gets around those reasons.
/// </summary>
/// <param name="pCaller">Pointer to caller object (AX).</param>
/// <param name="szURL">String of the URL.</param>
/// <param name="szFileName">String of the destination filename/path.</param>
/// <param name="dwReserved">[reserved].</param>
/// <param name="lpfnCB">A callback function to monitor progress or abort.</param>
/// <returns>0 for okay.</returns>
[DllImport("urlmon.dll", CharSet=CharSet.Auto, SetLastError=true)]
static extern Int32 URLDownloadToFile(
    [MarshalAs(UnmanagedType.IUnknown)] object pCaller,
    [MarshalAs(UnmanagedType.LPWStr)] string szURL,
    [MarshalAs(UnmanagedType.LPWStr)] string szFileName,
    Int32 dwReserved,
    IntPtr lpfnCB);
// This version maps HRESULT to exception:
[DllImport("urlmon.dll", CharSet=CharSet.Auto, PreserveSig=false)]
private static extern void URLDownloadToFile(
    [MarshalAs(UnmanagedType.IUnknown)] object pCaller,
    [MarshalAs(UnmanagedType.LPTStr)] string szURL,
    [MarshalAs(UnmanagedType.LPTStr)] string szFileName,
    Int32 dwReserved,
    IntPtr lpfnCB);
```

## VB Signature:
```cs
'Visual Basic 6.0
Public Declare Function URLDownloadToFileA Lib "urlmon" (ByVal pCaller As Long, ByVal szURL As String, ByVal szFileName As String, ByVal dwReserved As Long, ByVal lpfnCB As Long) As Long

'Visual Basic .NET
<DllImport("urlmon.dll", CharSet := CharSet.Auto, SetLastError := True)> _
Private Shared Function URLDownloadToFile(<MarshalAs(UnmanagedType.IUnknown)> pCaller As Object, <MarshalAs(UnmanagedType.LPWStr)> szURL As String, <MarshalAs(UnmanagedType.LPWStr)> szFileName As String, dwReserved As Int32, lpfnCB As IntPtr) As Int32
End Function
```

## Sample Code:
```cs
int response = URLDownloadToFile( null, urlStr, fileToStoreStr, 0, IntPtr.Zero );
    // For the second version:
    URLDownloadToFile(IE as SHDocVw.IWebBrowser2, urlStr, fileToStoreStr, 0, IntPtr.Zero );
```

## Alternative Managed API:
```cs
If (My.Computer.Network.IsAvailable) Then
        My.Computer.Network.DownloadFile("http://www.pinvoke.net/", "C:\Temp\pinvoke.htm")
    Else
        MsgBox("Network not found!")
    End If
```
