
## C++ Signature:
```cs
TCHAR volumeName[MAX_PATH + 1] = { 0 };
    TCHAR fileSystemName[MAX_PATH + 1] = { 0 };
    DWORD serialNumber = 0;
    DWORD maxComponentLen = 0;
    DWORD fileSystemFlags = 0;
    if (GetVolumeInformation(
        _T("C:\\"),
        volumeName,
        ARRAYSIZE(volumeName),
        &serialNumber,
        &maxComponentLen,
        &fileSystemFlags,
        fileSystemName,
        ARRAYSIZE(fileSystemName)))
    {
        m_sn_textbox.Format(_T("GetVolumeInformation : %lu"),serialNumber);
    }
```

## C# Signature:
```cs
[DllImport("Kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
  [return: MarshalAs(UnmanagedType.Bool)]
  public extern static bool GetVolumeInformation(
    string rootPathName,
    StringBuilder volumeNameBuffer,
    int volumeNameSize,
    out uint volumeSerialNumber,
    out uint maximumComponentLength,
    out FileSystemFeature fileSystemFlags,
    StringBuilder fileSystemNameBuffer,
    int nFileSystemNameSize);
```

## VB Signature:
```cs
Private Declare Auto Function GetVolumeInformation Lib "kernel32.dll" ( _
     ByVal RootPathName As String, _
     ByVal VolumeNameBuffer As System.Text.StringBuilder, _
     ByVal VolumeNameSize As UInt32, _
     ByRef VolumeSerialNumber As UInt32, _
     ByRef MaximumComponentLength As UInt32, _
     ByRef FileSystemFlags As UInt32, _
     ByVal FileSystemNameBuffer As System.Text.StringBuilder, _
     ByVal FileSystemNameSize As UInt32) As UInt32
```

## User-Defined Types:
```cs
[Flags]
  public enum FileSystemFeature : uint {
    /// <summary>
    /// The file system preserves the case of file names when it places a name on disk.
    /// </summary>
    CasePreservedNames = 2,

    /// <summary>
    /// The file system supports case-sensitive file names.
    /// </summary>
    CaseSensitiveSearch = 1,

    /// <summary>
    /// The specified volume is a direct access (DAX) volume. This flag was introduced in Windows 10, version 1607.
    /// </summary>
    DaxVolume = 0x20000000,

    /// <summary>
    /// The file system supports file-based compression.
    /// </summary>
    FileCompression = 0x10,

    /// <summary>
    /// The file system supports named streams.
    /// </summary>
    NamedStreams = 0x40000,

    /// <summary>
    /// The file system preserves and enforces access control lists (ACL).
    /// </summary>
    PersistentACLS = 8,

    /// <summary>
    /// The specified volume is read-only.
    /// </summary>
    ReadOnlyVolume = 0x80000,

    /// <summary>
    /// The volume supports a single sequential write.
    /// </summary>
    SequentialWriteOnce = 0x100000,

    /// <summary>
    /// The file system supports the Encrypted File System (EFS).
    /// </summary>
    SupportsEncryption = 0x20000,

    /// <summary>
    /// The specified volume supports extended attributes. An extended attribute is a piece of
    /// application-specific metadata that an application can associate with a file and is not part
    /// of the file's data.
    /// </summary>
    SupportsExtendedAttributes = 0x00800000,

    /// <summary>
    /// The specified volume supports hard links. For more information, see Hard Links and Junctions.
    /// </summary>
    SupportsHardLinks = 0x00400000,

    /// <summary>
    /// The file system supports object identifiers.
    /// </summary>
    SupportsObjectIDs = 0x10000,

    /// <summary>
    /// The file system supports open by FileID. For more information, see FILE_ID_BOTH_DIR_INFO.
    /// </summary>
    SupportsOpenByFileId = 0x01000000,

    /// <summary>
    /// The file system supports re-parse points.
    /// </summary>
    SupportsReparsePoints = 0x80,

    /// <summary>
    /// The file system supports sparse files.
    /// </summary>
    SupportsSparseFiles = 0x40,

    /// <summary>
    /// The volume supports transactions.
    /// </summary>
    SupportsTransactions = 0x200000,

    /// <summary>
    /// The specified volume supports update sequence number (USN) journals. For more information,
    /// see Change Journal Records.
    /// </summary>
    SupportsUsnJournal = 0x02000000,

    /// <summary>
    /// The file system supports Unicode in file names as they appear on disk.
    /// </summary>
    UnicodeOnDisk = 4,

    /// <summary>
    /// The specified volume is a compressed volume, for example, a DoubleSpace volume.
    /// </summary>
    VolumeIsCompressed = 0x8000,

    /// <summary>
    /// The file system supports disk quotas.
    /// </summary>
    VolumeQuotas = 0x20
  }
```

## Sample Code:
```cs
StringBuilder volname = new StringBuilder(261);
StringBuilder fsname = new StringBuilder(261);
uint sernum, maxlen;
FileSystemFeature flags;
if(!GetVolumeInformation("c:\\", volname, volname.Capacity, out sernum, out maxlen, out flags, fsname, fsname.Capacity))
    Marshal.ThrowExceptionForHR(Marshal.GetHRForLastWin32Error());
string volnamestr = volname.ToString();
string fsnamestr = fsname.ToString();
```

## Sample code - VB.NET:
```cs
''' <summary>
   ''' Returns volume name and serial number, maximum path component length, and filesystem name and flags
   ''' for the specified directory. Works with UNC. Can throw an exception.
   ''' </summary>
   ''' <param name="FolderPath">Path to drive or shared folder to find about.</param>
   ''' <param name="VolumeName">Returns volume name.</param>
   ''' <param name="VolumeSerialNumber">Returns volume serial number.</param>
   ''' <param name="MaxComponentLength">Returns max. path component lenght.</param>
   ''' <param name="FileSystemFlags">Returns file system flags - see http://msdn.microsoft.com/en-us/library/aa364993(VS.85).aspx</param>
   ''' <param name="FileSystemName">Returns file system name.</param>
   ''' <remarks></remarks>
   Public Sub GetVolumeInfo( _
     ByVal FolderPath As String, _
     ByRef VolumeName As String, _
     ByRef VolumeSerialNumber As String, _
     ByRef MaxComponentLength As UInt32, _
     ByRef FileSystemFlags As UInt32, _
     ByRef FileSystemName As String)
      ' see http://msdn.microsoft.com/en-us/library/aa364993(VS.85).aspx
      Dim sRootFolder As String = IO.Path.GetPathRoot(FolderPath)
      If Not sRootFolder.EndsWith("\") Then sRootFolder &= "\"
      Const MAX_PATH As Integer = &H104
      Dim volname As New System.Text.StringBuilder(MAX_PATH + 1)
      Dim fsname As New System.Text.StringBuilder(MAX_PATH + 1)
      Dim sernum As UInt32
      Dim RetVal As UInt32 = GetVolumeInformation(sRootFolder, volname, volname.Capacity, _
                          sernum, MaxComponentLength, FileSystemFlags, _
                          fsname, fsname.Capacity)
      If RetVal = 0 Then Throw New System.ComponentModel.Win32Exception(Err.LastDllError)
      VolumeName = volname.ToString
      FileSystemName = fsname.ToString

      Dim hpart, lpart As Integer
      hpart = sernum \ 65536
      lpart = sernum - hpart * 65536L
      VolumeSerialNumber = Hex(hpart).PadLeft(4, "0"c) & "-" & Hex(lpart).PadLeft(4, "0"c)
   End Sub
```

## Sample:
```cs
'Check for valid drive letter argument. 
    Dim ValidDriveLetters As String = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    If ValidDriveLetters.IndexOf(DriveLetter) <> -1 Then
    If DriveLetter.Length = 1 Then
        Dim Disk As New System.Management.ManagementObject("Win32_LogicalDisk.DeviceID=""" & DriveLetter & ":""")
        Dim DiskProperty As System.Management.PropertyData
        For Each DiskProperty In Disk.Properties
        If DiskProperty.Name = "VolumeSerialNumber" Then
            Return DiskProperty.Value.ToString  '.ToString 'Return the volume serial number. 
        End If
        Next DiskProperty
    End If
    End If
    Return Nothing 'Invalid drive letter.
```
