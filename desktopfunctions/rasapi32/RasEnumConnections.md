
## C# Signature:
```cs
[DllImport("rasapi32.dll", SetLastError = true, CharSet = CharSet.Auto)]
public static extern int RasEnumConnections(
    [In, Out] RASCONN[] rasconn,
    [In, Out] ref int cb,
    [Out] out int connections);
```

## VB Signature:
```cs
TODO
```

## User-Defined Types:
```cs
const int RAS_MaxEntryName = 256;
const int RAS_MaxDeviceType = 16;
const int RAS_MaxDeviceName = 128;
const int MAX_PATH = 260;
const int ERROR_BUFFER_TOO_SMALL = 603;
const int ERROR_SUCCESS = 0;

[StructLayout(LayoutKind.Sequential, Pack = 4, CharSet = CharSet.Auto)]
public struct RASCONN
{
    public int dwSize;
    public IntPtr hrasconn;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = RAS_MaxEntryName)]
    public string szEntryName;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = RAS_MaxDeviceType)]
    public string szDeviceType;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = RAS_MaxDeviceName)]
    public string szDeviceName;
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MAX_PATH)]
    public string szPhonebook;
    public int dwSubEntry;
    public Guid guidEntry;
    public int dwFlags;
    public Guid luid;                                                    
}
```

## Sample Code:
```cs
// create 1 item array.
RAW.RASCONN[] connections = new RAW.RASCONN[1];
connections[0].dwSize = Marshal.SizeOf(typeof(RAW.RASCONN));
//Get entries count
int connectionsCount = 0;
int cb = Marshal.SizeOf(typeof(RAW.RASCONN));
int nRet = RAW.RasEnumConnections(connections, ref cb, out connectionsCount);
if (nRet != RAW.ERROR_SUCCESS && nRet != RAW.ERROR_BUFFER_TOO_SMALL)
    throw new Win32Exception(nRet);
if (connectionsCount == 0)
    return;
// create array with specified entries number
connections = new RAW.RASCONN[connectionsCount];
for (int i = 0; i < connections.Length; i++)
{
    connections[i].dwSize = Marshal.SizeOf(typeof(RAW.RASCONN));
}
nRet = RAW.RasEnumConnections(connections, ref cb, out connectionsCount);
if (nRet != RAW.ERROR_SUCCESS)
    throw new Win32Exception((int)nRet);
```

## An alternative sample (Windows Vista or later) based on http://msdn.microsoft.com/en-us/library/aa377284(VS.85).aspx
```cs
int cb = 0, connectionCount;
if (RAW.RasEnumConnections(null, ref cb, out connectionCount) == RAW.ERROR_BUFFER_TOO_SMALL)
{
    if (connectionCount == 0) return;
    RAW.RASCONN[] buffer = new RAW.RASCONN[conns];
    buffer[0].dwSize = Marshal.SizeOf(typeof(RAW.RASCONN));
    if (RasApi.RasEnumConnections(buffer, ref cb, out conns) == RAW.ERROR_SUCCESS)
    {
        // look through the buffer...
    }
}
```
