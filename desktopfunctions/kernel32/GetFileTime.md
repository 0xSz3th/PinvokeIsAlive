
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool GetFileTime(IntPtr hFile, IntPtr lpCreationTime,
   IntPtr lpLastAccessTime, IntPtr lpLastWriteTime);
```

## VB.Net Signature:
```cs
<DllImport( _
            "kernel32.dll", _
            CharSet:=CharSet.Auto, _
            SetLastError:=True)> _
         Friend Shared Function GetFileTime( _
                        ByVal hFile As IntPtr, _
                        <Out()> ByRef lpCreationTime As FILETIME, _
                        <Out()> ByRef lpLastAccessTime As FILETIME, _
                        <Out()> ByRef lpLastWriteTime As FILETIME) _
                    As Boolean
        End Function
```

## Sample Code:
```cs
public class GetFileTimeSample
{
    private const uint GENERIC_READ = 0x80000000;
    private const uint FILE_SHARE_READ = 0x1;
    private const uint FILE_ATTRIBUTE_NORMAL = 0x80;
    private const int INVALID_HANDLE_VALUE = -1;
    private const uint OPEN_EXISTING = 3;

    [StructLayout(LayoutKind.Sequential)]
    private struct FILETIME
    {
    public uint dwLowDateTime;
    public uint dwHighDateTime;
    }

    [DllImport("kernel32.dll", SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern bool CloseHandle(
    IntPtr hObject
    );

    [DllImport("kernel32.dll", CharSet = CharSet.Auto, CallingConvention = CallingConvention.StdCall, SetLastError = true)]
    private static extern IntPtr CreateFile(
    string lpFileName,
    uint dwDesiredAccess,
    uint dwShareMode,
    IntPtr SecurityAttributes,
    uint dwCreationDisposition,
    uint dwFlagsAndAttributes,
    IntPtr hTemplateFile
    );

    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern bool GetFileTime(
    IntPtr hFile,
    ref FILETIME lpCreationTime,
    ref FILETIME lpLastAccessTime,
    ref FILETIME lpLastWriteTime
    );

    public static void GetFileTimes(string FileName, out DateTime CreationTime, out DateTime LastAccessTime, out DateTime LastWriteTime)
    {
    CreationTime = DateTime.MinValue;
    LastAccessTime = DateTime.MinValue;
    LastWriteTime = DateTime.MinValue;
    IntPtr ptr = IntPtr.Zero;
    FILETIME ftCreationTime = new FILETIME();
    FILETIME ftLastAccessTime = new FILETIME();
    FILETIME ftLastWriteTime = new FILETIME();
    try
    {
        ptr = CreateFile(FileName, GENERIC_READ, FILE_SHARE_READ, IntPtr.Zero, OPEN_EXISTING, FILE_ATTRIBUTE_NORMAL, IntPtr.Zero);
        if (ptr.ToInt32() == INVALID_HANDLE_VALUE)
        Marshal.ThrowExceptionForHR(Marshal.GetHRForLastWin32Error());
        if (GetFileTime(ptr, ref ftCreationTime, ref ftLastAccessTime, ref ftLastWriteTime) != true)
        Marshal.ThrowExceptionForHR(Marshal.GetHRForLastWin32Error());
        CreationTime = DateTime.FromFileTimeUtc((((long)ftCreationTime.dwHighDateTime) << 32) | ((uint)ftCreationTime.dwLowDateTime));
        LastAccessTime = DateTime.FromFileTimeUtc((((long)ftLastAccessTime.dwHighDateTime) << 32) | ((uint)ftLastAccessTime.dwLowDateTime));
        LastWriteTime = DateTime.FromFileTimeUtc((((long)ftLastWriteTime.dwHighDateTime) << 32) | ((uint)ftLastWriteTime.dwLowDateTime)); 
    }
    catch (Exception e)
    {
        throw (e);
    }
    finally
    {
        if (ptr !=IntPtr.Zero && ptr.ToInt32() != INVALID_HANDLE_VALUE) CloseHandle(ptr);
    }
    }
}
```
