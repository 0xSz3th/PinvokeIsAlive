
## C# Definition:
```cs
public delegate uint PTHREAD_START_ROUTINE( IntPtr lpThreadParameter );

[StructLayout( LayoutKind.Sequential )]
public struct CREATE_PROCESS_DEBUG_INFO
{
   public IntPtr hFile;
   public IntPtr hProcess;
   public IntPtr hThread;
   public IntPtr lpBaseOfImage;
   public uint dwDebugInfoFileOffset;
   public uint nDebugInfoSize;
   public IntPtr lpThreadLocalBase;
   public PTHREAD_START_ROUTINE lpStartAddress;
   public IntPtr lpImageName;
   public ushort fUnicode;
}
```
