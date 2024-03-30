
## C# Signature:
```cs
[DllImport("Dbghelp.dll")]
static extern bool MiniDumpWriteDump(IntPtr hProcess, uint ProcessId, IntPtr hFile, int DumpType, ref MINIDUMP_EXCEPTION_INFORMATION ExceptionParam, IntPtr UserStreamParam, IntPtr CallbackParam);
```

## VB Signature:
```cs
Declare Function MiniDumpWriteDump Lib "Dbghelp.dll" (TODO) As TODO
```

## Sample Code:
```cs
[DllImport("Dbghelp.dll")]
static extern bool MiniDumpWriteDump(IntPtr hProcess, uint ProcessId, IntPtr hFile, int DumpType,
    ref MINIDUMP_EXCEPTION_INFORMATION ExceptionParam, IntPtr UserStreamParam, IntPtr CallbackParam);

[DllImport("kernel32.dll")]
static extern IntPtr GetCurrentProcess();

[DllImport("kernel32.dll")]
static extern uint GetCurrentProcessId();

[DllImport("kernel32.dll")]
static extern uint GetCurrentThreadId();

[StructLayout(LayoutKind.Sequential, Pack = 4)]
public struct MINIDUMP_EXCEPTION_INFORMATION
{
    public uint ThreadId;
    public IntPtr ExceptionPointers;
    public int ClientPointers;
}

/// <summary>
/// Call back function that will be called when an exception has occured. This function will create
/// a fullmemory dump of the application
/// </summary>
/// <param name="sender"></param>
/// <param name="e"></param>
static void CurrentDomain_UnhandledException(object sender, UnhandledExceptionEventArgs e)
{
    string assemblyPath = Assembly.GetEntryAssembly().Location;
    string dumpFileName = assemblyPath + "_" + DateTime.Now.ToString("dd.MM.yyyy.HH.mm.ss") + ".dmp";
    FileStream file = new FileStream(dumpFileName, FileMode.Create);
    MINIDUMP_EXCEPTION_INFORMATION info = new MINIDUMP_EXCEPTION_INFORMATION();
    info.ClientPointers = 1;
    info.ExceptionPointers = Marshal.GetExceptionPointers();
    info.ThreadId = GetCurrentThreadId();
    // A full memory dump is necessary in the case of a managed application, other wise no information
    // regarding the managed code will be available
    MiniDumpWriteDump( GetCurrentProcess(), GetCurrentProcessId(), file.SafeFileHandle.DangerousGetHandle(),
    MiniDumpWithFullMemory, ref info, IntPtr.Zero, IntPtr.Zero );
    file.Close();
    string exeName = Path.GetFileName(assemblyPath);
    MessageBox.Show( "An Unhanled exception has been detected in the application " + exeName +
    " .\r\nException information is saved in " + dumpFileName, "Error", MessageBoxButton.OK, MessageBoxImage.Error);
}

private static readonly int MiniDumpWithFullMemory = 2;
```
