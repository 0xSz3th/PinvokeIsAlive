
## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
public struct DataTypesInfo {
    [MarshalAs(UnmanagedType.LPTStr)]
    public string Name;
}
```

## Sample Code:
```cs
public static class PrintProcessor {

    public enum ServerEnvironment{
    X86,
    X64,
    Ia64,
    Local,
    }

    [DllImport("winspool.drv", CharSet = CharSet.Auto, SetLastError = true)]
    private static extern bool EnumPrintProcessorDatatypes(string name,
    string printProcessorName, UInt32 level, IntPtr dataTypesBuf,
    UInt32 bufSize, ref UInt32 bytesNeeded, ref UInt32 numStructsReturned);

    private const int ErrorInsufficientBuffer = 0x7a;

    public static IEnumerable<string> GetPrintProcessorDataTypes(string printProcessorName) {
    return GetPrintProcessorDataTypes(string.Empty, printProcessorName);
    }

    public static IEnumerable<string> GetPrintProcessorDataTypes(string serverName, string printProcessorName) {
    uint bytesNeeded = 0;
    uint numStructsReturned = 0;

    //first call gets the number of bytes and structures needed - it must return an ErrorInsufficientBuffer error
    if (EnumPrintProcessorDatatypes(serverName, printProcessorName, 1, IntPtr.Zero, 0, ref bytesNeeded, ref numStructsReturned)) {
        return null;
    }

    int lastWin32Error = Marshal.GetLastWin32Error();

    if (lastWin32Error == ErrorInsufficientBuffer) {
        IntPtr rawBuffer = Marshal.AllocHGlobal((int)bytesNeeded);
        try {
        if (EnumPrintProcessorDatatypes(serverName, printProcessorName, 1, rawBuffer, bytesNeeded, ref bytesNeeded, ref numStructsReturned)) {
            var dataTypesInfoArray = new DataTypesInfo[numStructsReturned];
            int offset = rawBuffer.ToInt32();
            Type type = typeof(DataTypesInfo);
            int increment = Marshal.SizeOf(type);
            for (int i = 0; i < numStructsReturned; i++) {
            dataTypesInfoArray[i] = (DataTypesInfo)Marshal.PtrToStructure(new IntPtr(offset), type);
            offset += increment;
            }

            var retStrings = new List<string>();
            foreach (var dataTypeInfo in dataTypesInfoArray) {
            retStrings.Add(dataTypeInfo.Name);
            }
            return retStrings;
        }
        } finally {
        Marshal.FreeHGlobal(rawBuffer);
        }
        //lastWin32Error = Marshal.GetLastWin32Error();
    }
    //if I get here - it's an error, so...

    return null;
    }

    private static string GetEnvironmentString(ServerEnvironment environment) {
    switch (environment) {
        case ServerEnvironment.X86:
        return "Windows x86";
        case ServerEnvironment.X64:
        return "Windows x64";
        case ServerEnvironment.Ia64:
        return "Windows IA64";
        case ServerEnvironment.Local:
        return string.Empty;
    }
    //not really needed, but...
    return string.Empty;
    }
}
```
