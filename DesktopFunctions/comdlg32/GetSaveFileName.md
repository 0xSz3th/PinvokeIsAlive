
## C# Signature:
```cs
[DllImport("Comdlg32.dll", CharSet=CharSet.Auto, SetLastError=true)]
private static extern bool GetSaveFileName(ref OPENFILENAME lpofn);
```

## VB.NET Signature:
```cs
<DllImport("Comdlg32.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
Private Shared Function GetSaveFileName(ByRef lpofn As OPENFILENAME) As Boolean
End Function
```

## Sample Code:
```cs
' Copyright
    ' Microsoft Corporation
    ' All rights reserved

    'typedef struct tagOFN {
    '  DWORD     lStructSize;
    '  HWND      hwndOwner;
    '  HINSTANCE     hInstance;
    '  LPCTSTR       lpstrFilter;
    '  LPTSTR    lpstrCustomFilter;
    '  DWORD     nMaxCustFilter;
    '  DWORD     nFilterIndex;
    '  LPTSTR    lpstrFile;
    '  DWORD     nMaxFile;
    '  LPTSTR    lpstrFileTitle;
    '  DWORD     nMaxFileTitle;
    '  LPCTSTR       lpstrInitialDir;
    '  LPCTSTR       lpstrTitle;
    '  DWORD     Flags;
    '  WORD      nFileOffset;
    '  WORD      nFileExtension;
    '  LPCTSTR       lpstrDefExt;
    '  LPARAM    lCustData;
    '  LPOFNHOOKPROC lpfnHook;
    '  LPCTSTR       lpTemplateName;
    '#if (_WIN32_WINNT >= 0x0500)
    '  void *    pvReserved;
    '  DWORD     dwReserved;
    '  DWORD     FlagsEx;
    '#endif // (_WIN32_WINNT >= 0x0500)
    '} OPENFILENAME, *LPOPENFILENAME;

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
    Public Class OpenFileName

    Public structSize As Integer = 0
    Public dlgOwner As IntPtr = IntPtr.Zero
    Public instance As IntPtr = IntPtr.Zero
    Public filter As String = Nothing
    Public customFilter As String = Nothing
    Public maxCustFilter As Integer = 0
    Public filterIndex As Integer = 0
    Public file As String = Nothing
    Public maxFile As Integer = 0
    Public fileTitle As String = Nothing
    Public maxFileTitle As Integer = 0
    Public initialDir As String = Nothing
    Public title As String = Nothing
    Public flags As Integer = 0
    Public fileOffset As Short = 0
    Public fileExtension As Short = 0
    Public defExt As String = Nothing
    Public custData As IntPtr = IntPtr.Zero
    Public hook As IntPtr = IntPtr.Zero
    Public templateName As String = Nothing
    Public reservedPtr As IntPtr = IntPtr.Zero
    Public reservedInt As Integer = 0
    Public flagsEx As Integer = 0

    End Class 'OpenFileName

    Public Class LibWrap
    'BOOL GetOpenFileName(LPOPENFILENAME lpofn);
    Declare Auto Function GetSaveFileName Lib "Comdlg32.dll" ( _
    <[In](), Out()> ByVal ofn As OpenFileName) As Boolean
    End Class 'LibWrap

    Private Function ShowOpen(Optional ByVal filter As String = ("All files" & ChrW(0) & "*.*" & ChrW(0)), _    
          Optional ByVal title As String = "Save File Dialog...", _
          Optional ByVal defext As String = "*", _
          Optional ByVal path As String = "C:\") As String

    Try
    Dim ofn As New OpenFileName

    ofn.structSize = Marshal.SizeOf(ofn)
    ofn.filter = filter
    ofn.file = New String(New Char(256) {})
    ofn.maxFile = ofn.file.Length
    ofn.fileTitle = New String(New Char(64) {})
    ofn.maxFileTitle = ofn.fileTitle.Length
    ofn.initialDir = path
    ofn.title = title
    ofn.defExt = defext

    If LibWrap.GetSaveFileName(ofn) Then
        Return ofn.file
    End If
    Catch ex As Exception
    Debug.Assert(False)
    Return System.String.Empty
    End Try

    End Function
```
