
## C# Signature:
```cs
[DllImport(@"User32", SetLastError=true, EntryPoint = "RegisterPowerSettingNotification",
         CallingConvention = CallingConvention.StdCall)]
    private static extern IntPtr RegisterPowerSettingNotification(
        IntPtr hRecipient,
        ref Guid PowerSettingGuid,
        Int32 Flags);
```

## VB Signature:
```cs
Declare Function RegisterPowerSettingNotification Lib "user32.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
private const int WM_POWERBROADCAST = 0x0218;

    static Guid GUID_BATTERY_PERCENTAGE_REMAINING = new Guid("A7AD8041-B45A-4CAE-87A3-EECBB468A9E1");
    static Guid GUID_MONITOR_POWER_ON = new Guid(0x02731015, 0x4510, 0x4526, 0x99, 0xE6, 0xE5, 0xA1, 0x7E, 0xBD, 0x1A, 0xEA);
    static Guid GUID_ACDC_POWER_SOURCE = new Guid(0x5D3E9A59, 0xE9D5, 0x4B00, 0xA6, 0xBD, 0xFF, 0x34, 0xFF, 0x51, 0x65, 0x48);
    static Guid GUID_POWERSCHEME_PERSONALITY = new Guid(0x245D8541, 0x3943, 0x4422, 0xB0, 0x25, 0x13, 0xA7, 0x84, 0xF6, 0x79, 0xB7);
    static Guid GUID_MAX_POWER_SAVINGS = new Guid(0xA1841308, 0x3541, 0x4FAB, 0xBC, 0x81, 0xF7, 0x15, 0x56, 0xF2, 0x0B, 0x4A);
    // No Power Savings - Almost no power savings measures are used.
    static Guid GUID_MIN_POWER_SAVINGS = new Guid(0x8C5E7FDA, 0xE8BF, 0x4A96, 0x9A, 0x85, 0xA6, 0xE2, 0x3A, 0x8C, 0x63, 0x5C);
    // Typical Power Savings - Fairly aggressive power savings measures are used.
    static Guid GUID_TYPICAL_POWER_SAVINGS = new Guid(0x381B4222, 0xF694, 0x41F0, 0x96, 0x85, 0xFF, 0x5B, 0xB2, 0x60, 0xDF, 0x2E);
```

## User-Defined Types:
```cs
// Win32 decls and defs
    //
    const int PBT_APMQUERYSUSPEND = 0x0000;
    const int PBT_APMQUERYSTANDBY = 0x0001;
    const int PBT_APMQUERYSUSPENDFAILED = 0x0002;
    const int PBT_APMQUERYSTANDBYFAILED = 0x0003;
    const int PBT_APMSUSPEND = 0x0004;
    const int PBT_APMSTANDBY = 0x0005;
    const int PBT_APMRESUMECRITICAL = 0x0006;
    const int PBT_APMRESUMESUSPEND = 0x0007;
    const int PBT_APMRESUMESTANDBY = 0x0008;
    const int PBT_APMBATTERYLOW = 0x0009;
    const int PBT_APMPOWERSTATUSCHANGE = 0x000A; // power status
    const int PBT_APMOEMEVENT = 0x000B;
    const int PBT_APMRESUMEAUTOMATIC = 0x0012;
    const int PBT_POWERSETTINGCHANGE = 0x8013; // DPPE
```

## User-Defined Types:
```cs
const int DEVICE_NOTIFY_WINDOW_HANDLE = 0x00000000;
    const int DEVICE_NOTIFY_SERVICE_HANDLE = 0x00000001;

    // This structure is sent when the PBT_POWERSETTINGSCHANGE message is sent.
    // It describes the power setting that has changed and contains data about the change
    [StructLayout(LayoutKind.Sequential, Pack = 4)]
    internal struct POWERBROADCAST_SETTING
    {
        public Guid PowerSetting;
        public uint DataLength;
        public byte Data;
    }
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 4)]
    internal struct POWERBROADCAST_SETTING {
        public Guid PowerSetting;
        public uint DataLength;
        // public byte Data;    // (*1)
    }

    private void RegisterForPowerNotifications(IntPtr hwnd)
    {
        hPowerSrc = RegisterPowerSettingNotification(hwnd,
        ref GUID_ACDC_POWER_SOURCE,
        DEVICE_NOTIFY_WINDOW_HANDLE);

        hBattCapacity = RegisterPowerSettingNotification(hwnd,
        ref GUID_BATTERY_PERCENTAGE_REMAINING,
        DEVICE_NOTIFY_WINDOW_HANDLE);

        hMonitorOn = RegisterPowerSettingNotification(hwnd,
        ref GUID_MONITOR_POWER_ON,
        DEVICE_NOTIFY_WINDOW_HANDLE);

        hPowerScheme = RegisterPowerSettingNotification(hwnd,
        ref GUID_POWERSCHEME_PERSONALITY,
        DEVICE_NOTIFY_WINDOW_HANDLE);
    }

    private static IntPtr WndProc(IntPtr hwnd, int msg, IntPtr wParam, IntPtr lParam, ref bool handled)
    {
        if (msg == WM_POWERBROADCAST && wParam.ToInt32() == PBT_POWERSETTINGCHANGE)
        {
        // Extract data from message
        POWERBROADCAST_SETTING ps =
         (POWERBROADCAST_SETTING)Marshal.PtrToStructure(
             lParam, typeof(POWERBROADCAST_SETTING));
        IntPtr pData = (IntPtr)(lParam.ToInt32() + Marshal.SizeOf(ps));  // (*1)

        // Examine notification

        if (ps.PowerSetting == GUID_POWERSCHEME_PERSONALITY &&
            ps.DataLength == Marshal.SizeOf(typeof(Guid)))
        {
            // New power scheme selected.

            Guid newPersonality =
            (Guid)Marshal.PtrToStructure(pData, typeof(Guid));

            if (newPersonality == GUID_MAX_POWER_SAVINGS)
            {
            personality = PowerPersonality.Savings;
            }
            else if (newPersonality == GUID_MIN_POWER_SAVINGS)
            {
            personality = PowerPersonality.Performance;
            }
            else if (newPersonality == GUID_TYPICAL_POWER_SAVINGS)
            {
            personality = PowerPersonality.Mixed;
            }
            else
            {
            Debug.WriteLine("switched to unknown Power savings");
            personality = PowerPersonality.Mixed;
            }
        }
        else if (ps.PowerSetting == GUID_ACDC_POWER_SOURCE &&
             ps.DataLength == Marshal.SizeOf(typeof(Int32)))
        {
            Int32 iData = (Int32)Marshal.PtrToStructure(pData, typeof(Int32));
            Debug.WriteLine("ACDC: " + iData);

            onBattery = iData != 0;
        }
```
