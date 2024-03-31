
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi, Pack = 2)]
public struct MIXERLINETARGET
{
     private UInt32 dwType;
     private UInt32 dwDeviceID;
     private UInt16 wMid;
     private UInt16 wPid;
     private UInt32 vDriverVersion;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = MixerXPNative.MAXPNAMELEN)]
     private string szPname;

     #region Properties

     /// <summary>MIXERLINE_TARGETTYPE_xxxx</summary>
     public MIXERLINE_TARGETTYPE Type
     {
        get { return (MIXERLINE_TARGETTYPE)this.dwType; }
        set { this.dwType = (UInt32)value; }
     }
     /// <summary>target device ID of device type</summary>
     public UInt32 DeviceID
     {
        get { return this.dwDeviceID; }
        set { this.dwDeviceID = value; }
     }
     /// <summary>of target device</summary>
     public UInt16 ManufacturerID
     {
        get { return this.wMid; }
        set { this.wMid = value; }
     }
     /// <summary></summary>
     public UInt16 ProductID
     {
        get { return this.wPid; }
        set { this.wPid = value; }
     }
     /// <summary></summary>
     public UInt32 DriverVersion
     {
        get { return this.vDriverVersion; }
        set { this.vDriverVersion = value; }
     }
     /// <summary></summary>
     public string PName
     {
        get { return this.szPname; }
        set { this.szPname = value; }
     }

     #endregion
}
```

## VB Definition:
```cs
Structure MIXERLINETARGET
  Dim dwType As AudioLineType
  Dim dwDeviceId As UInteger
  Dim wMid As UShort
  Dim wPid As UShort
  Dim vDriverVersion As UInteger
  <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAXPNAMELEN)> Dim szPName As String
End Structure
```
