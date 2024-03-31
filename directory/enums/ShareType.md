
## C# Definition:
```cs
public enum SHARE_TYPE : uint
    {
        STYPE_DISK = 0,  // Disk Share
        STYPE_PRINTQ = 1,    // Print Queue
        STYPE_DEVICE = 2,    // Communication Device 
        STYPE_IPC = 3,       // IPC (Interprocess communication) Share
        STYPE_HIDDEN_DISK = 0x80000000,  // Admin Disk Shares
        STYPE_HIDDEN_PRINT = 0x80000001,  // Admin Print Shares
        STYPE_HIDDEN_DEVICE = 0x80000002,  // Admin Device Shares
        STYPE_HIDDEN_IPC = 0x80000003,  // Admin IPC Shares
        // Need to add flags for 
        // STYPE_TEMPORARY
    }
```

## VB Definition:
```cs
#Region "SHARE_TYPE Enumeration Definition"
    ' <summary>Type of share</summary>
    Public Enum ShareType
      ' <summary>Disk Share</summary>
      Disk = 0
      ' <summary>Printer Share</summary>
      Printer = 1
      ' <summary>Device Share</summary>
      Device = 2
      ' <summary>IPC Share</summary>
      IPC = 3
      ' <summary>Special Share</summary>
      ' <remarks>
      ' Add this value to one of the above values
      ' to get an Administrative Share of that type
      ' </remarks>
      Special = &H80000000
    End Enum
  #End Region
```
