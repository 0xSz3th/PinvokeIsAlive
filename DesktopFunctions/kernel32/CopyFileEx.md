
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool CopyFileEx(string lpExistingFileName, string lpNewFileName,
   CopyProgressRoutine lpProgressRoutine, IntPtr lpData, ref Int32 pbCancel, 
   CopyFileFlags dwCopyFlags);
```

## VB.NET Signature:
```cs
Private Declare Auto Function CopyFileEx Lib "kernel32.dll" (ByVal lpExistingFileName As String, _
     ByVal lpNewFileName As String, ByVal lpProgressRoutine As CopyProgressRoutine, _
     ByVal lpData As IntPtr, ByRef pbCancel As Boolean, _
     ByVal dwCopyFlags As CopyFileFlags) As <MarshalAs(UnmanagedType.Bool)> Boolean
```

## Sample C# Code:
```cs
[DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    [return: MarshalAs(UnmanagedType.Bool)]
    static extern bool CopyFileEx(string lpExistingFileName, string lpNewFileName,
       CopyProgressRoutine lpProgressRoutine, IntPtr lpData, ref Int32 pbCancel,
       CopyFileFlags dwCopyFlags);

    delegate CopyProgressResult CopyProgressRoutine(
    long TotalFileSize,
    long TotalBytesTransferred,
    long StreamSize,
    long StreamBytesTransferred,
    uint dwStreamNumber,
    CopyProgressCallbackReason dwCallbackReason,
    IntPtr hSourceFile,
    IntPtr hDestinationFile,
    IntPtr lpData);

    int pbCancel;

    enum CopyProgressResult : uint
    {
        PROGRESS_CONTINUE = 0,
        PROGRESS_CANCEL = 1,
        PROGRESS_STOP = 2,
        PROGRESS_QUIET = 3
    }

    enum CopyProgressCallbackReason : uint
    {
        CALLBACK_CHUNK_FINISHED = 0x00000000,
        CALLBACK_STREAM_SWITCH = 0x00000001
    }

    [Flags]
    enum CopyFileFlags : uint
    {
        COPY_FILE_FAIL_IF_EXISTS = 0x00000001,
        COPY_FILE_RESTARTABLE = 0x00000002,
        COPY_FILE_OPEN_SOURCE_FOR_WRITE = 0x00000004,
        COPY_FILE_ALLOW_DECRYPTED_DESTINATION = 0x00000008
    }

    private void XCopy(string oldFile, string newFile)
    {
        CopyFileEx(oldFile, newFile, new CopyProgressRoutine(this.CopyProgressHandler), IntPtr.Zero, ref pbCancel, CopyFileFlags.COPY_FILE_RESTARTABLE);
    }

    private CopyProgressResult CopyProgressHandler(long total, long transferred, long streamSize, long StreamByteTrans, uint dwStreamNumber,CopyProgressCallbackReason reason, IntPtr hSourceFile, IntPtr hDestinationFile, IntPtr lpData)
    {
        return CopyProgressResult.PROGRESS_CONTINUE;
    }
```

## Sample VB.NET Code:
```cs
Public Class CopyFile_Ex

    Private Declare Auto Function CopyFileEx Lib "kernel32.dll" (ByVal lpExistingFileName As String, _
        ByVal lpNewFileName As String, ByVal lpProgressRoutine As CopyProgressRoutine, _
        ByVal lpData As IntPtr, ByRef pbCancel As Boolean, _
        ByVal dwCopyFlags As CopyFileFlags) As <MarshalAs(UnmanagedType.Bool)> Boolean

    Private Delegate Function CopyProgressRoutine(ByVal TotalFileSize As Long, _
        ByVal TotalBytesTransferred As Long, ByVal StreamSize As Long, ByVal StreamBytesTransferred As Long, _
        ByVal dwStreamNumber As UInteger, ByVal dwCallbackReason As CopyProgressCallbackReason, _
        ByVal hSourceFile As IntPtr, ByVal hDestinationFile As IntPtr, ByVal lpData As IntPtr) As CopyProgressResult

    Private CopyExSyncObject As New Object

    Private pbCancel As Boolean = False
    Private sourcePath As String
    Private destPath As String
    Private overWrite As Boolean
    Private complete As Boolean
    Private totalBytes As Int64
    Private ammountTransfered As Double

    Private Enum CopyProgressResult As UInteger
        PROGRESS_CONTINUE = 0
        PROGRESS_CANCEL = 1
        PROGRESS_STOP = 2
        PROGRESS_QUIET = 3
    End Enum

    Private Enum CopyProgressCallbackReason As UInteger
        CALLBACK_CHUNK_FINISHED = &H0
        CALLBACK_STREAM_SWITCH = &H1
    End Enum

    <Flags()> _
    Private Enum CopyFileFlags As UInteger
        COPY_FILE_FAIL_IF_EXISTS = &H1
        COPY_FILE_RESTARTABLE = &H2
        COPY_FILE_OPEN_SOURCE_FOR_WRITE = &H4
        COPY_FILE_ALLOW_DECRYPTED_DESTINATION = &H8
    End Enum

    Private Function GetFilenameFromPath(ByVal filePath As String, _
                Optional ByVal errMsg As String = "") As String

        If filePath.Contains("\") Then
        Dim parts() As String
        parts = Split(filePath, "\")
        Return parts(parts.Length - 1)
        Else
        Return ""
        End If

    End Function

    Public Sub New(ByVal _sourcePath As String, ByVal _destPath As String, ByVal _overWrite As Boolean)
        complete = True
        CopyEx(_sourcePath, _destPath, _overWrite)
    End Sub

    Public Sub New()
        complete = True
    End Sub

    Public Function GetBytesTransfered() As Int64
        SyncLock CopyExSyncObject
        GetBytesTransfered = CLng(ammountTransfered)
        End SyncLock
    End Function

    Public Function GetPercentComplete() As Integer
        SyncLock CopyExSyncObject
        GetPercentComplete = CInt((ammountTransfered / totalBytes) * 100)
        End SyncLock
    End Function

    Public Sub Cancel()
        SyncLock CopyExSyncObject
        pbCancel = True
        End SyncLock
    End Sub

    Public Function IsComplete() As Boolean
        SyncLock CopyExSyncObject
        IsComplete = complete
        End SyncLock
    End Function

    Public Sub CopyEx(ByVal _sourcePath As String, ByVal _destPath As String, ByVal _overWrite As Boolean)

        If Not complete Then Exit Sub

        sourcePath = _sourcePath
        destPath = _destPath
        overWrite = _overWrite
        complete = False

        totalBytes = 0
        ammountTransfered = 0

        Dim _theFilesInfo As New FileInfo(sourcePath)
        totalBytes = _theFilesInfo.Length

        Dim copyThread As New Threading.Thread(AddressOf StartCopy)
        copyThread.Start()

    End Sub

    Private Sub StartCopy()
        If overWrite Then
        CopyFileEx(sourcePath, destPath, New CopyProgressRoutine(AddressOf CopyProgressHandler), IntPtr.Zero, pbCancel, CopyFileFlags.COPY_FILE_OPEN_SOURCE_FOR_WRITE)
        Else
        CopyFileEx(sourcePath, destPath, New CopyProgressRoutine(AddressOf CopyProgressHandler), IntPtr.Zero, pbCancel, CopyFileFlags.COPY_FILE_FAIL_IF_EXISTS)
        End If
        complete = True
    End Sub

    Private Function CopyProgressHandler(ByVal total As Long, ByVal transferred As Long, ByVal streamSize As Long, ByVal StreamByteTrans As Long, ByVal dwStreamNumber As UInteger, ByVal reason As CopyProgressCallbackReason, _
     ByVal hSourceFile As IntPtr, ByVal hDestinationFile As IntPtr, ByVal lpData As IntPtr) As CopyProgressResult

        SyncLock CopyExSyncObject
        ammountTransfered = transferred
        End SyncLock

        If pbCancel Then
        complete = True
        ammountTransfered = 0
        pbCancel = False
        Return CopyProgressResult.PROGRESS_CANCEL
        Else
        Return CopyProgressResult.PROGRESS_CONTINUE
        End If

    End Function

    End Class
```
