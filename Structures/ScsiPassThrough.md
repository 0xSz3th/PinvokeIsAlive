
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public class ScsiPassThrough {
        /// <summary>The size of the item passed to DeviceIoControl</summary>
        public ushort Length;

        /// <summary>The status of the SCSI command</summary>
        public byte ScsiStatus;

        /// <summary>The SCSI bus</summary>
        public byte PathId;

        /// <summary>The SCSI target</summary>
        public byte TargetId;

        /// <summary>The SCSI lun</summary>
        public byte Lun;

        /// <summary>The number of bytes in the CDB field</summary>
        public byte CdbLength;

        /// <summary>How long the sense info structure is</summary>
        public byte SenseInfoLength;

        /// <summary>Usually set to SCSI_IOCTL_DATA_IN</summary>
        public byte DataIn;

        /// <summary>How many bytes to transfer</summary>
        public UInt32 DataTransferLength;

        /// <summary>How long to wait before timing out</summary>
        public UInt32 TimeOutValue;

        /// <summary>The offset of the data buffer area returned</summary>
        public IntPtr DataBufferOffset; // UInt32 does not work on 64-bit

        /// <summary>The offset of the sense info returned</summary>
        public UInt32 SenseInfoOffset;

        /// <summary>The command code to send to the robot</summary>
        [MarshalAs(UnmanagedType.ByValArray, SizeConst=16)]
        public byte[] Cdb;
```

## VB Definition:
```cs
Structure ScsiPassThrough 
   Public TODO
End Structure
```

## Notes:
```cs
/// <summary>
/// Constructor for the command to send to the device
/// </summary>
/// <param name="target">The SCSI target</param>
/// <param name="bus">The SCSI bus</param>
/// <param name="lun">The SCSI lun</param>
/// <param name="cdbLen">The length of the CDB to be sent</param>
/// <param name="dataTransferLength">The length to use</param>
public ScsiPassThrough(byte target, byte bus, byte lun, byte cdbLen, UInt32 dataTransferLength) {
    Length = (ushort) Marshal.SizeOf(typeof(ScsiPassThrough));
    ScsiStatus = 0;
    PathId = bus;
    TargetId = target;
    Lun = lun;
    CdbLength = cdbLen;
    SenseInfoLength = 24;
    DataIn = 1;    // SCSI_IOCTL_DATA_IN
    DataTransferLength = dataTransferLength;
    TimeOutValue = 200;
    DataBufferOffset = Marshal.OffsetOf(typeof ScsiPassThroughWithBuffers), "ucDataBuf");
    SenseInfoOffset = (uint) Marshal.OffsetOf(typeof ScsiPassThroughWithBuffers), "ucSenseBuf");
    Cdb = new byte[16] {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};
}
```
