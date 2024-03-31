
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct MIB_TCPROW_OWNER_PID
{
    public uint state;
    public uint localAddr;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public byte[] localPort;
    public uint remoteAddr;
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public byte[] remotePort;
    public uint owningPid;

    public uint ProcessId
    {
        get { return owningPid; }
    }

    public IPAddress LocalAddress
    {
        get { return new IPAddress(localAddr); }
    }

    public ushort LocalPort
    {
        get
        {
            return BitConverter.ToUInt16(new byte[2] { localPort[1], localPort[0] }, 0);
        }
    }

    public IPAddress RemoteAddress
    {
        get { return new IPAddress(remoteAddr); }
    }

    public ushort RemotePort
    {
        get
        {
            return BitConverter.ToUInt16( new byte[2] { remotePort[1], remotePort[0] }, 0);
        }
    }

    public MIB_TCP_STATE State
    {
        get { return (MIB_TCP_STATE)state; }
    }
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure MIB_TCPROW_OWNER_PID
    Public m_state As UInteger
    Public localAddr As UInteger
    <MarshalAs(UnmanagedType.ByValArray, SizeConst := 4)> _
    Public m_localPort As Byte()
    Public remoteAddr As UInteger
    <MarshalAs(UnmanagedType.ByValArray, SizeConst := 4)> _
    Public m_remotePort As Byte()
    Public owningPid As UInteger

    Public ReadOnly Property ProcessId() As UInteger
        Get
            Return owningPid
        End Get
    End Property

    Public ReadOnly Property LocalAddress() As IPAddress
        Get
            Return New IPAddress(localAddr)
        End Get
    End Property

    Public ReadOnly Property LocalPort() As UShort
        Get
            Return BitConverter.ToUInt16(New Byte(1) {m_localPort(1), m_localPort(0)}, 0)
        End Get
    End Property

    Public ReadOnly Property RemoteAddress() As IPAddress
        Get
            Return New IPAddress(remoteAddr)
        End Get
    End Property

    Public ReadOnly Property RemotePort() As UShort
        Get
            Return BitConverter.ToUInt16(New Byte(1) {m_remotePort(1), m_remotePort(0)}, 0)
        End Get
    End Property

    Public ReadOnly Property State() As MIB_TCP_STATE
        Get
            Return DirectCast(m_state, MIB_TCP_STATE)
        End Get
    End Property
End Structure
```

## Notes:
```cs
Ports are broken up by bytes. (This is the same as the standard library does it). High order by is returned first.   Port 139 would be represented as  localPort1 =0, localPort2=139, localPort3=0, localPort4=0, where as 5800 would be localPort1=22, localPort2=168, etc...,   MSDN shows these as being DWORD.
```
