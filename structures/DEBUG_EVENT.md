
## C# Definition:
```cs
enum DebugEventType : uint
  {
    RIP_EVENT = 9,
    OUTPUT_DEBUG_STRING_EVENT = 8,
    UNLOAD_DLL_DEBUG_EVENT = 7,
    LOAD_DLL_DEBUG_EVENT = 6,
    EXIT_PROCESS_DEBUG_EVENT = 5,
    EXIT_THREAD_DEBUG_EVENT = 4,
    CREATE_PROCESS_DEBUG_EVENT = 3,
    CREATE_THREAD_DEBUG_EVENT = 2,
    EXCEPTION_DEBUG_EVENT = 1,
  }

  [StructLayout(LayoutKind.Sequential)]
  public struct DEBUG_EVENT
  {
  public DebugEventType dwDebugEventCode;
  public int dwProcessId;
  public int dwThreadId;

  [MarshalAs(UnmanagedType.ByValArray, SizeConst = 86, ArraySubType = UnmanagedType.U1)]
  byte[] debugInfo;

  public EXCEPTION_DEBUG_INFO Exception{
    get { return GetDebugInfo<EXCEPTION_DEBUG_INFO>(); }
  }

  public CREATE_THREAD_DEBUG_INFO CreateThread
  {
    get { return GetDebugInfo<CREATE_THREAD_DEBUG_INFO>(); }
  }

  public CREATE_PROCESS_DEBUG_INFO CreateProcessInfo
  {
    get { return GetDebugInfo<CREATE_PROCESS_DEBUG_INFO>(); }
  }

  public EXIT_THREAD_DEBUG_INFO ExitThread
  {
    get { return GetDebugInfo<EXIT_THREAD_DEBUG_INFO>(); }
  }

  public EXIT_PROCESS_DEBUG_INFO ExitProcess
  {
    get { return GetDebugInfo<EXIT_PROCESS_DEBUG_INFO>(); }
  }

  public LOAD_DLL_DEBUG_INFO LoadDll
  {
    get { return GetDebugInfo<LOAD_DLL_DEBUG_INFO>(); }
  }

  public UNLOAD_DLL_DEBUG_INFO UnloadDll
  {
    get { return GetDebugInfo<UNLOAD_DLL_DEBUG_INFO>(); }
  }

  public OUTPUT_DEBUG_STRING_INFO DebugString
  {
    get { return GetDebugInfo<OUTPUT_DEBUG_STRING_INFO>(); }
  }

  public RIP_INFO RipInfo
  {
    get { return GetDebugInfo<RIP_INFO>(); }
  }

  private T GetDebugInfo<T>() where T : struct
  {
    var structSize = Marshal.SizeOf(typeof(T));
    var pointer = Marshal.AllocHGlobal(structSize);
    Marshal.Copy(debugInfo, 0, pointer, structSize);

    var result = Marshal.PtrToStructure(pointer, typeof(T));
    Marshal.FreeHGlobal(pointer);
    return (T)result;
  }
}
```
