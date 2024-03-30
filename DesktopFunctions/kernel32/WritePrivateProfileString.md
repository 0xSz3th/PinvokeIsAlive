
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Unicode, SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool WritePrivateProfileString(string lpAppName,
   string lpKeyName, string lpString, string lpFileName);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
Private Shared Function WritePrivateProfileString(ByVal lpAppName As String, _
                        ByVal lpKeyName As String, _
                        ByVal lpString As String, _
                        ByVal lpFileName As String) As Boolean
    End Function
```

## VB.NET Alternative Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
Private Declare Auto Function WritePrivateProfileString Lib "kernel32" (ByVal lpAppName As String, _    
                        ByVal lpKeyName As String, _
                        ByVal lpString As String, _
                        ByVal lpFileName As String) As Boolean
```

## C++ Signature:
```cs
[DllImport("KERNEL32.DLL", CharSet=CharSet::Auto, EntryPoint="WritePrivateProfileString")]
static Boolean WritePrivateProfileString(String^ lpAppName, String^ lpKeyName, String^ lpString, String^ lpFileName);
```

## Sample Code:
```cs
bool Return;
    Return = WritePrivateProfileString(SectionName,
                       KeyName,
                       StringToWrite,
                       INIFileName);
    return Return;
```

## Sample Code:
```cs
Dim bres As Boolean
bres = WritePrivateProfileString("AppName", "KeyName", "TestValue", "c:\test.ini")
Console.WriteLine("WritePrivateProfileString returned : " & bres.ToString())
```

## Sample Code:
```cs
Public Function WriteIni(ByVal lpAppName As String, ByVal lpKeyName As String, ByVal lpString As String, ByVal lpFilename As String) As Boolean
     Try

     WritePrivateProfileString(lpAppname, lpKeyName, lpString, lpFilename)
     Return True
     Exit Try

     Catch ex As Exception

     Return False

     End Try
End Function
```

## Sample Code:
```cs
http://gallery.technet.microsoft.com/scriptcenter/Edit-old-fashioned-INI-f8fbc067
```
