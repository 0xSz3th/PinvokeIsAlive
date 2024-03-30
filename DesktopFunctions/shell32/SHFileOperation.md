
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet = CharSet.Auto, SetLastError = true, ThrowOnUnmappableChar = true)]
static extern int SHFileOperation(ref SHFILEOPSTRUCT lpFileOp);
```

## VB.NET Signature:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Auto, SetLastError:=true, ThrowOnUnmappableChar:=true)> _
Public Function SHFileOperation(<MarshalAs(UnmanagedType.Struct)>ByRef lpFileOp As SHFILEOPSTRUCT) As Integer
End function
```

## VB Signature
```cs
Public Declare Function SHFileOperation Lib "shell32" Alias "SHFileOperationA" _
        (lpFileOp As SHFILEOPSTRUCT) As Long
```

## Tips & Tricks:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 1, CharSet = CharSet.Auto)]
public struct SHFILEOPSTRUCT32
{
   public IntPtr hwnd;
   public uint wFunc;
   [MarshalAs(UnmanagedType.LPTStr)]
   public string pFrom;
   [MarshalAs(UnmanagedType.LPTStr)]
   public string pTo;
   public ushort fFlags;
   public bool fAnyOperationsAborted;
   public IntPtr hNameMappings;
   [MarshalAs(UnmanagedType.LPTStr)]
   public string lpszProgressTitle;
}

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct SHFILEOPSTRUCT64
{
   public IntPtr hwnd;
   public uint wFunc;
   [MarshalAs(UnmanagedType.LPTStr)]
   public string pFrom;
   [MarshalAs(UnmanagedType.LPTStr)]
   public string pTo;
   public ushort fFlags;
   public bool fAnyOperationsAborted;
   public IntPtr hNameMappings;
   [MarshalAs(UnmanagedType.LPTStr)]
   public string lpszProgressTitle;
}

[DllImport("shell32.dll", EntryPoint = "SHFileOperation", CharSet = CharSet.Auto, SetLastError = true, ThrowOnUnmappableChar = true)]
static extern int SHFileOperation32(ref SHFILEOPSTRUCT32 lpFileOp);

[DllImport("shell32.dll", EntryPoint = "SHFileOperation", CharSet = CharSet.Auto, SetLastError = true, ThrowOnUnmappableChar = true)]
static extern int SHFileOperation64(ref SHFILEOPSTRUCT64 lpFileOp);

public unsafe void SendToRecycleBin(string path, bool silent = true)
{
   var flags = FILEOP_FLAGS.FOF_ALLOWUNDO;
   if (silent) { flags |= FILEOP_FLAGS.FOF_SILENT | FILEOP_FLAGS.FOF_NOCONFIRMATION; }

   if (sizeof(IntPtr) == 4)
   {
     var data = new SHFILEOPSTRUCT32
     {
       wFunc = (uint)FileFuncFlags.FO_DELETE,
       pFrom = path + '\0',
       fFlags = (ushort)flags
     };
     SHFileOperation32(ref data);
   }
   else
   {
     var data = new SHFILEOPSTRUCT64
     {
       wFunc = (uint)FileFuncFlags.FO_DELETE,
       pFrom = path + '\0',
       fFlags = (ushort)flags
     };
     SHFileOperation64(ref data);
   }
}
```

## Alternative Managed API:
```cs
Microsoft.VisualBasic.FileIO.FileSystem.DeleteFile(string, Microsoft.VisualBasic.FileIO.UIOption, Microsoft.VisualBasic.FileIO.RecycleOption);
```
