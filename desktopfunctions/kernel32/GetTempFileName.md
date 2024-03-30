
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint GetTempFileName(string lpPathName, string lpPrefixString,
   uint uUnique, [Out] StringBuilder lpTempFileName);
```

## Tips & Tricks:
```cs
/// <summary>
/// The GetTempFileName and GetTempFolderName methods (and overloads) provide
/// the same level of convenience as the managed Path.GetTempFileName (including
/// support for folders), but provide access to the Win32 functionality of providing
/// an optional prefix, unique suffix and base folder name, as well as the Win32
/// functionality of creating the temp file or folder as soon as the name is generated.
/// </summary>
class Win32Utility {
  [DllImport("kernel32.dll", SetLastError = true)]
  static extern uint GetTempFileName(string lpPathName, string lpPrefixString, uint uUnique, [Out] StringBuilder lpTempFileName);

  public static string GetTempFileName() {
    return GetTempFileName("tmp");
  }

  public static string GetTempFileName(string prefix) {
    return GetTempFileName(prefix, 0);
  }

  public static string GetTempFileName(string prefix, uint unique) {
    return GetTempFileName(prefix, unique, Path.GetTempPath());
  }

  public static string GetTempFileName(string prefix, uint unique, string basePath) {

    // 260 is MAX_PATH in Win32 windows.h header
    // 'sb' needs >0 size else GetTempFileName throws IndexOutOfRangeException.  260 is the most you'd want.
    StringBuilder sb = new StringBuilder(260);     

    uint result = GetTempFileName(basePath, prefix, unique, sb);
    if( result == 0 ) {
      throw new Exception("Win32 Error: " + System.Runtime.InteropServices.Marshal.GetLastWin32Error());
    }

    return sb.ToString();
  }

  public static string GetTempFolderName() {
    return GetTempFolderName("tmp");
  }

  public static string GetTempFolderName(string prefix) {
    return GetTempFolderName(prefix, 0);
  }

  public static string GetTempFolderName(string prefix, uint unique) {
    return GetTempFolderName(prefix, unique, Path.GetTempPath());
  }

  public static string GetTempFolderName(string prefix, uint unique, string basePath) {
    string tempFolderName = GetTempFileName(prefix, unique, basePath);
    if( unique == 0 ) {
      // Delete created file and create folder name instead
      File.Delete(tempFolderName);
      Directory.CreateDirectory(tempFolderName);
    }

    return tempFolderName;
  }
}
```

## Sample Code:
```cs
string tempFile = Win32Utility.GetTempFileName();
...
File.Delete(tempFile);

string tempFolder = Win32Utility.GetTempFolderName();
...
Folder.Delete(tempFolder);
```

## Alternative Managed API:
```cs
System.IO.Path 

[Visual Basic]
Public Shared Function GetTempFileName() As String

[C#]
public static string GetTempFileName();

[C++]
public: static String* GetTempFileName();

[JScript]
public static function GetTempFileName() : String;
```
