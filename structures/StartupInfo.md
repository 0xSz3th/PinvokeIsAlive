
## C# Definition:
```cs
// This also works with CharSet.Ansi as long as the calling function uses the same character set.
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct STARTUPINFOEX
{
     public STARTUPINFO StartupInfo;
     public IntPtr lpAttributeList;
}

// This also works with CharSet.Ansi as long as the calling function uses the same character set.
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
struct STARTUPINFO
{
     public Int32 cb;
     public string lpReserved;
     public string lpDesktop;
     public string lpTitle;
     public Int32 dwX;
     public Int32 dwY;
     public Int32 dwXSize;
     public Int32 dwYSize;
     public Int32 dwXCountChars;
     public Int32 dwYCountChars;
     public Int32 dwFillAttribute;
     public Int32 dwFlags;
     public Int16 wShowWindow;
     public Int16 cbReserved2;
     public IntPtr lpReserved2;
     public IntPtr hStdInput;
     public IntPtr hStdOutput;
     public IntPtr hStdError;
}

// If you are using this with [GetStartupInfo], this definition works without errors.
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
struct STARTUPINFO
{
     public Int32 cb;
     public IntPtr lpReserved;
     public IntPtr lpDesktop;
     public IntPtr lpTitle;
     public Int32 dwX;
     public Int32 dwY;
     public Int32 dwXSize;
     public Int32 dwYSize;
     public Int32 dwXCountChars;
     public Int32 dwYCountChars;
     public Int32 dwFillAttribute;
     public Int32 dwFlags;
     public Int16 wShowWindow;
     public Int16 cbReserved2;
     public IntPtr lpReserved2;
     public IntPtr hStdInput;
     public IntPtr hStdOutput;
     public IntPtr hStdError;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Unicode)>
Public Structure STARTUPINFOEX 
   Public StartupInfo As STARTUPINFO
   Public lpAttributeList As IntPtr
End Structure

  <StructLayout(LayoutKind.Sequential)> _
  Public Structure STARTUPINFO
   Public cb As Integer
   Public lpReserved As String
   Public lpDesktop As String
   Public lpTitle As String
   Public dwX As Integer
   Public dwY As Integer
   Public dwXSize As Integer
   Public dwYSize As Integer
   Public dwXCountChars As Integer
   Public dwYCountChars As Integer
   Public dwFillAttribute As Integer
   Public dwFlags As Integer
   Public wShowWindow As Short
   Public cbReserved2 As Short
   Public lpReserved2 As Integer
   Public hStdInput As Integer
   Public hStdOutput As Integer
   Public hStdError As Integer
  End Structure
```

## Notes:
```cs
startupInfoEx.StartupInfo.cb = Marshal.SizeOf(startupInfoEx);
```
