
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool SetFileTime(IntPtr hFile, ref long lpCreationTime, ref long lpLastAccessTime, ref long lpLastWriteTime);
```

## VB.Net Signature:
```cs
<DllImport("kernel32.dll", SetLastError := True)> _
Private Shared Function SetFileTime(ByVal hFile As IntPtr, ByRef lpCreationTime As Long, ByRef lpLastAccessTime As Long, ByRef lpLastWriteTime As Long) As Boolean
End Function
```

## C# Sample Code:
```cs
public static void SetFileTimes(IntPtr hFile, DateTime creationTime, DateTime accessTime, DateTime writeTime)
  {
    long lCreationTime    = creationTime.ToFileTime();
    long lAccessTime    = accessTime.ToFileTime();
    long lWriteTime        = writeTime.ToFileTime();

    if(!SetFileTime(hFile, ref lCreationTime, ref lAccessTime, ref lWriteTime))
    {
        throw new Win32Exception();
    }
  }
```

## VB.Net Sample Code:
```cs
''' -----------------------------------------------------------------------------
    ''' <summary>
    ''' Will transfer the Time Stamps from the Source file to the Target file.
    ''' </summary>
    ''' <param name="oSource_File_Info">The file that the time stamps will be transfered from.</param>
    ''' <param name="oTarget_File_Info">The file that the time stamps will be transfered to.</param>
    ''' <remarks>
    ''' Will transfer the Time Stamps from the Source file to the Target file.
    ''' </remarks>
    ''' <history>
    '''     [CHope]    3/2/2006    Created
    ''' </history>
    ''' -----------------------------------------------------------------------------
    Public Shared Sub Synchronize_Time_Stamps(ByVal oSource_File_Info As System.IO.FileInfo, ByVal oTarget_File_Info As System.IO.FileInfo)

    Dim oFile_Stream As System.IO.FileStream

    ' Open The File So The Time Stamps Can Be Updated
    oFile_Stream = System.IO.File.Open(oTarget_File_Info.FullName, System.IO.FileMode.Open, System.IO.FileAccess.Write)

    ' Call The API That Should Set The Time Stamps For The File
    If Not SetFileTime(oFile_Stream.Handle, oSource_File_Info.CreationTime.ToFileTime, oSource_File_Info.LastAccessTime.ToFileTime,     oSource_File_Info.LastWriteTime.ToFileTime) Then

        System.Windows.Forms.MessageBox.Show("Unable to set " & oTarget_File_Info.Name & " time stamps.", "Synchronization Error")

    End If

    ' Close The Stream
    oFile_Stream.Close()

    End Sub
```
