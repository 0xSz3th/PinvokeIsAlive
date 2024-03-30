
## User-Defined Types:
```cs
[Flags]
    public enum SendDataFlags
    {
    /// <summary></summary>
    None = 0,
    /// <summary>    Specifies that the data should not be subject to routing. A Windows Sockets service provider can choose to ignore this flag</summary>
    DontRoute = 1,
    /// <summary>Sends OOB data (stream-style socket such as SOCK_STREAM only)</summary>
    OOB = 2
    }

    /// <summary>Структура адреса для сокета</summary>
    [StructLayout(LayoutKind.Sequential)]
    public struct SockAddr
    {
    /// <summary>Семейство протоколов</summary>
    public short Family;
    /// <summary>Номер порта для сокета</summary>
    public ushort Port;
    /// <summary>Локальный IP адрес сокета</summary>
    public AddressIP4 IPAddress;
    /// <summary>8 байт для выравнивания структуры</summary>
    private Int64 Zero;

    public SockAddr (short Family, ushort Port, AddressIP4 IP)
    { this.Family = Family; this.Port = Port; this.IPAddress = IP; this.Zero = 0; }
    }

    /// <summary>IP адресс</summary>
    [StructLayout(LayoutKind.Sequential)]
    public struct AddressIP4
    {
    /// <summary>Первый байт IP адреса</summary>
    public byte a1;
    /// <summary>Второй байт IP адреса</summary>
    public byte a2;
    /// <summary>Третий байт IP адреса</summary>
    public byte a3;
    /// <summary>Четвертый байт IP адреса</summary>
    public byte a4;

    /// <summary>Широковещательный IP адрес</summary>
    public static AddressIP4 Broadcast { get { return new AddressIP4 (255,255,255,255); } }
    /// <summary>Любой IP адрес</summary>
    public static AddressIP4 AnyAddress { get { return new AddressIP4 (0,0,0,0); } }
    /// <summary>IP адрес локального хоста</summary>
    public static AddressIP4 Loopback { get { return new AddressIP4 (127,0,0,1); } }

    public AddressIP4 (byte a1, byte a2, byte a3, byte a4)
    { this.a1 = a1; this.a2 = a2; this.a3 = a3; this.a4 = a4; }
    }
```
