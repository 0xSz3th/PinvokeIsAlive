
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct STARTUPINFOEX
{
     public STARTUPINFO StartupInfo;
     public IntPtr lpAttributeList;
}
```

## VB Definition:
```cs
Structure STARTUPINFOEX 
   Public TODO
End Structure
```

## Notes:
```cs
startupInfoEx.StartupInfo.cb = Marshal.SizeOf(startupInfoEx);
```
