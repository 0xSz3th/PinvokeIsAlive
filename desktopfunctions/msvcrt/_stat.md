
## C# Signature:
```cs
[DllImport("msvcrt.dll", SetLastError = true, CallingConvention = CallingConvention.Cdecl)]
    static extern int _stat(string file, ref STAT buf);
```

## VB Signature:
```cs
Declare Function _stat Lib "msvcrt.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct STAT
    {
      public uint     st_dev;
      public ushort     st_ino;
      public ushort st_mode;
      public short      st_nlink;
      public short      st_uid;
      public short      st_gid;
      public uint    st_rdev;
      public uint    st_size;
      public uint st_atime;
      public uint st_mtime;
      public uint st_ctime;
    }
```

## Sample Code:
```cs
STAT s = new STAT();
    int res = _stat(file, ref s);
    if (res != 0)
    {
      int errcode = Marshal.GetLastWin32Error();
      string errorMessage = new Win32Exception(errcode).Message;
      Console.WriteLine("Error '" + errcode + "': " +errorMessage);            
    } else {
      //[...]
    }
```
