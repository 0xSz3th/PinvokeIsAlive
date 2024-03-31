
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct COMMPROP
{
    ushort wPacketLength;
    ushort wPacketVersion;
    uint dwServiceMask;
    uint dwReserved1;
    uint dwMaxTxQueue;
    uint dwMaxRxQueue;
    uint dwMaxBaud;
    uint dwProvSubType;
    uint dwProvCapabilities;
    uint dwSettableParams;
    uint dwSettableBaud;
    ushort wSettableData;
    ushort wSettableStopParity;
    uint dwCurrentTxQueue;
    uint dwCurrentRxQueue;
    uint dwProvSpec1;
    uint dwProvSpec2;
    ushort wcProvChar; //original type is WCHAR[1]
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)>
    Structure COMMPROP
    Dim wPacketLength As Short
    Dim wPacketVersion As Short
    Dim dwServiceMask As Integer
    Dim dwReserved1 As Integer
    Dim dwMaxTxQueue As Integer
    Dim dwMaxRxQueue As Integer
    Dim dwMaxBaud As Integer
    Dim dwProvSubType As Integer
    Dim dwProvCapabilities As Integer
    Dim dwSettableParams As Integer
    Dim dwSettableBaud As Integer
    Dim wSettableData As Short
    Dim wSettableStopParity As Short
    Dim dwCurrentTxQueue As Integer
    Dim dwCurrentRxQueue As Integer
    Dim dwProvSpec1 As Integer
    Dim dwProvSpec2 As Integer
    <VBFixedArray(1)> Dim wcProvChar() As Short

    Public Sub Initialize()
        ReDim wcProvChar(1)
    End Sub
    End Structure
```
