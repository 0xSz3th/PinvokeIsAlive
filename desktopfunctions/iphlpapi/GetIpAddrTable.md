[DllImport("iphlpapi.dll", SetLastError=true)]
public static extern int GetIpAddrTable(IntPtr pIpAddrTable, ref int pdwSize, bool bOrder);
Declare Ansi Function 
GetIpAddrTable Lib "iphlpapi.dll" (ByRef ipTable As IntPtr, ByRef tableSize As IntPtr, ByVal ordered As Boolean) As UInt32
[DllImport(S"IPHLPAPI.DLL", EntryPoint=S"GetIpAddrTable", SetLastError=true, CharSet=CharSet::Unicode, ExactSpelling=true)]
static UInt32 GetIpAddressTable( [Out] IntPtr ipTable, [In,Out] IntPtr tableSize, bool sort);
System.Net.Dns.GetHostAddresses()

## Example:
```cs
foreach (System.Net.IPAddress strIP in System.Net.Dns.GetHostAddresses(System.Net.Dns.GetHostName()))
  {
    Console.WriteLine(strIP.ToString());
  }
```

## Example:
```cs
IntPtr pBuf = IntPtr.Zero;
int nBufSize = 0;
// get the required buffer size            
GetIpAddrTable( IntPtr.Zero, ref nBufSize, false );
// allocate the buffer
pBuf = Marshal.AllocHGlobal( nBufSize );
int r = GetIpAddrTable( pBuf, ref nBufSize, false );
if ( r != 0 )
    throw new System.ComponentModel.Win32Exception( r );

int entrySize = Marshal.SizeOf(typeof(MIB_IPADDRROW));
int nEntries = Marshal.ReadInt32(pBuf);
int tableStartAddr = (int)pBuf + sizeof(int);
for (int i = 0; i < nEntries; i++)
{
    IntPtr pEntry = (IntPtr)(tableStartAddr + i * entrySize);
    MIB_IPADDRROW addrStruct = (MIB_IPADDRROW)Marshal.PtrToStructure(pEntry, typeof(MIB_IPADDRROW));
    string ipAddrStr = IPToString( IPAddress.NetworkToHostOrder((int)addrStruct._address) );
    string ipMaskStr = IPToString( IPAddress.NetworkToHostOrder((int)addrStruct._mask) );
}
if ( pBuf != IntPtr.Zero )
    Marshal.FreeHGlobal( pBuf );

// helper function IPToString
static string IPToString(int ipaddr)
{
    return String.Format( "{0}.{1}.{2}.{3}",
    (ipaddr >> 24) & 0xFF, (ipaddr >> 16) & 0xFF,
    (ipaddr >> 8) & 0xFF, ipaddr & 0xFF);
}
```
