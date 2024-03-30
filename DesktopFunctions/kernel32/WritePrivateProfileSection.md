
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool WritePrivateProfileSection(string lpAppName,
   string lpString, string lpFileName);
```

## C++ Signature:
```cs
[DllImport("KERNEL32.DLL", CharSet=CharSet::Auto, EntryPoint="WritePrivateProfileSection")]
static Boolean WritePrivateProfileSection(String^ lpAppName, String^ lpString, String^ lpFileName);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll")> _
Private Declare Auto Function WritePrivateProfileSection(ByVal lpAppName As String, _
   ByVal lpString As String, _
   ByVal lpFileName As String) As Boolean
```

## VB.NET Signature:
```cs
Lib "kernel32.dll" Alias "WritePrivateProfileStringA" _
      (ByVal lpApplicationName As String, _
      ByVal lpKeyName As String, ByVal lpString As String, _
      ByVal lpFileName As String) As Integer
```

## Sample Code:
```cs
Dim MYNAME As String = Replace(Replace(Replace(My.Application.Info.CompanyName.ToLower, ",", ""), ".", ""), " ", "_")
    Dim ConfigFile As String = Environment.GetFolderPath(Environment.SpecialFolder.CommonApplicationData) & "\" & MYNAME & "\" & "database.config"

   Private Declare Ansi Function GetPrivateProfileString _
      Lib "kernel32.dll" Alias "GetPrivateProfileStringA" _
      (ByVal lpApplicationName As String, _
      ByVal lpKeyName As String, ByVal lpDefault As String, _
      ByVal lpReturnedString As System.Text.StringBuilder, _
      ByVal nSize As Integer, ByVal lpFileName As String) _
      As Integer
    Private Declare Ansi Function WritePrivateProfileString _
      Lib "kernel32.dll" Alias "WritePrivateProfileStringA" _
      (ByVal lpApplicationName As String, _
      ByVal lpKeyName As String, ByVal lpString As String, _
      ByVal lpFileName As String) As Integer
    Private Declare Ansi Function GetPrivateProfileInt _
      Lib "kernel32.dll" Alias "GetPrivateProfileIntA" _
      (ByVal lpApplicationName As String, _
      ByVal lpKeyName As String, ByVal nDefault As Integer, _
      ByVal lpFileName As String) As Integer
    Private Declare Ansi Function FlushPrivateProfileString _
      Lib "kernel32.dll" Alias "WritePrivateProfileStringA" _
      (ByVal lpApplicationName As Integer, _
      ByVal lpKeyName As Integer, ByVal lpString As Integer, _
      ByVal lpFileName As String) As Integer

Public Sub New()
    Dim FI As New FileInfo(ConfigFile)
    If My.Computer.FileSystem.DirectoryExists(FI.DirectoryName) = False Then
        My.Computer.FileSystem.CreateDirectory(FI.DirectoryName)
    End If

    If My.Computer.FileSystem.FileExists(ConfigFile) = False Then
        CreateIniDefaults()
    End If

    If GetString("SETTINGS", "LAST", "") = "0" Then
        CreateIniDefaults()
    End If
```

## Sample Code:
```cs
End Sub
```

## Sample Code:
```cs
Public Function GetString(ByVal Section As String, ByVal Key As String, ByVal [Default] As String) As String
    ' Returns a string from your INI file
    Dim intCharCount As Integer = 0
    Dim objResult As New System.Text.StringBuilder(1024)
    intCharCount = GetPrivateProfileString(Section, Key, [Default], objResult, objResult.Capacity, ConfigFile)
    If intCharCount > 0 Then
        GetString = Left(objResult.ToString, intCharCount)
    Else
        Return "0"
    End If
    End Function

    Public Function GetInteger(ByVal Section As String, _
      ByVal Key As String, ByVal [Default] As Integer) As Integer
    ' Returns an integer from your INI file
    Return GetPrivateProfileInt(Section, Key, _
       [Default], ConfigFile)
    End Function
```

## Sample Code:
```cs
Public Sub WriteString(ByVal Section As String, _
    ByVal Key As String, ByVal Value As String)
    ' Writes a string to your INI file
    WritePrivateProfileString(Section, Key, Value, ConfigFile)
    Flush()
    End Sub
    Public Sub WriteInteger(ByVal Section As String, _
      ByVal Key As String, ByVal Value As Integer)
    ' Writes an integer to your INI file
    WriteString(Section, Key, CStr(Value))
    Flush()
    End Sub
```

## Sample Code:
```cs
Private Sub Flush()
    ' Stores all the cached changes to your INI file
    FlushPrivateProfileString(0, 0, 0, ConfigFile)
    End Sub
```

## Sample Code:
```cs
Private Sub CreateIniDefaults()
    Dim FI As New FileInfo(ConfigFile)
    Dim s As String = String.Empty
    s = s & "[LAST]" & vbCrLf & "LAST=LOCAL" & vbCrLf & vbCrLf
    s = s & "[LOCAL]" & vbCrLf
    s = s & "DBTYPE=2" & vbCrLf
    s = s & "O1=127.0.0.1" & vbCrLf
    s = s & "ISADMIN=0" & vbCrLf
    s = s & vbCrLf & vbCrLf
    s = s & "[SETTINGS]" & vbCrLf
    s = s & "COMPANY=MY COMPANY,INC." & vbCrLf
    Try
        My.Computer.FileSystem.WriteAllText(ConfigFile, s, False)
    Catch ex As Exception
        MsgBox("Unable to save default database settings." & vbCrLf & ex.InnerException.ToString, MsgBoxStyle.Information)
    End Try
    End Sub
```
