
## C# Definition:
```cs
public delegate uint PTHREAD_START_ROUTINE( IntPtr lpThreadParameter );

[StructLayout( LayoutKind.Sequential )]
public struct CREATE_THREAD_DEBUG_INFO
{
   public IntPtr hThread;
   public IntPtr lpThreadLocalBase;
   public PTHREAD_START_ROUTINE lpStartAddress;
}
```
