
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 1, CharSet = CharSet.Auto)]
public struct SHFILEOPSTRUCT
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
```

## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct SHFILEOPSTRUCT
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
```

## VB.NET Definition
```cs
<StructLayout(LayoutKind.Sequential, Pack:=1, CharSet:=CharSet.Auto)> _
Public Structure SHFILEOPSTRUCT
     Public hwnd As IntPtr
     <MarshalAs(UnmanagedType.U4)>Public wFunc As FileFuncFlags
     <MarshalAs(UnmanagedType.LPTStr)>Public pFrom As String
     <MarshalAs(UnmanagedType.LPTStr)>Public pTo As String
     <MarshalAs(UnmanagedType.U2)>Public fFlags As FILEOP_FLAGS
     <MarshalAs(UnmanagedType.Bool)>Public fAnyOperationsAborted As Boolean
     Public hNameMappings As IntPtr
     <MarshalAs(UnmanagedType.LPTStr)>Public lpszProgressTitle As String '  only used if FOF_SIMPLEPROGRESS
End Structure
```

## VB.NET Definition
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> _
Public Structure SHFILEOPSTRUCT
     Public hwnd As IntPtr
     <MarshalAs(UnmanagedType.U4)>Public wFunc As FileFuncFlags
     <MarshalAs(UnmanagedType.LPTStr)>Public pFrom As String
     <MarshalAs(UnmanagedType.LPTStr)>Public pTo As String
     <MarshalAs(UnmanagedType.U2)>Public fFlags As FILEOP_FLAGS
     <MarshalAs(UnmanagedType.Bool)>Public fAnyOperationsAborted As Boolean
     Public hNameMappings As IntPtr
     <MarshalAs(UnmanagedType.LPTStr)>Public lpszProgressTitle As String '  only used if FOF_SIMPLEPROGRESS
End Structure
```

## VB Definition:
```cs
Public Type SHFILEOPSTRUCT
     hWnd As Long
     wFunc As FileFuncFlags
     pFrom As String
     pTo As String
     fFlags As FILEOP_FLAGS
     fAnyOperationsAborted As Long
     hNameMappings As Long
     lpszProgressTitle As String
End Type
```

## Alternative Managed API:
```cs
using Microsoft.VisualBasic.FileIO;
FileSystem.DeleteFile(path, UIOption.OnlyErrorDialogs, RecycleOption.SendToRecycleBin);
```
