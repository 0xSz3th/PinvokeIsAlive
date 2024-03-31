
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct MIB_TCP6ROW_OWNER_PID
{
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 16)]
    public byte[] localAddr;
    public uint localScopeId;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public byte[] localPort;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 16)]
    public byte[] remoteAddr;
    public uint remoteScopeId;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public byte[] remotePort;
    public uint state;
    public uint owningPid;

    public uint ProcessId
    {
        get { return owningPid; }
    }

    public long LocalScopeId
    {
        get { return localScopeId; }
    }

    public IPAddress LocalAddress
    {
        get { return new IPAddress(localAddr, LocalScopeId); }
    }

    public ushort LocalPort
    {
        get { return BitConverter.ToUInt16(localPort.Take(2).Reverse().ToArray(), 0); }
    }

    public long RemoteScopeId
    {
        get { return remoteScopeId; }
    }

    public IPAddress RemoteAddress
    {
        get { return new IPAddress(remoteAddr, RemoteScopeId); }
    }

    public ushort RemotePort
    {
        get { return BitConverter.ToUInt16(remotePort.Take(2).Reverse().ToArray(), 0); }
    }

    public MIB_TCP_STATE State
    {
        get { return (MIB_TCP_STATE)state; }
    }
}
```

## VB Definition:
```cs
Structure MIB_TCP6ROW_OWNER_PID 
   Public TODO
End Structure
```
