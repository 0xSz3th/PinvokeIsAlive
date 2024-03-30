
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool GetSystemPowerStatus(out SYSTEM_POWER_STATUS
   lpSystemPowerStatus);
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices; // Necessary!
```

## Sample Code:
```cs
namespace MyNamespace
{
    /// <summary>
    /// Summary description for BatteryChecker.
    /// </summary>
    public class BatteryChecker
    {
        public BatteryChecker()
        {
            // Nothing
        }

        [DllImport("Kernel32")]
        private static extern Boolean GetSystemPowerStatus( SystemPowerStatus sps );
```

## Sample Code:
```cs
public static SystemPowerStatus GetSystemPowerStatus()
        {
            SystemPowerStatus sps = new SystemPowerStatus();
            GetSystemPowerStatus( sps );
            return sps;
        }
    }

    public enum ACLineStatus : byte
    {
        Offline = 0, Online = 1, Unknown = 255
    }

    public enum BatteryFlag : byte
    {
        High = 1,
        Low = 2,
        Critical = 4,
        Charging = 8,
        NoSystemBattery = 128,
        Unknown = 255
    }

    // Fields must mirror their unmanaged counterparts, in order
    [StructLayout( LayoutKind.Sequential )]
    public class SystemPowerStatus
    {
        public ACLineStatus _ACLineStatus;
        public BatteryFlag  _BatteryFlag;
        public Byte     _BatteryLifePercent;
        public Byte     _Reserved1;
        public Int32    _BatteryLifeTime;
        public Int32    _BatteryFullLifeTime;
    }
}
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;
```

## Sample Code:
```cs
class SystemPower
{
    [DllImport("kernel32.dll", SetLastError = true)]
    private static extern Boolean GetSystemPowerStatus(out SystemPowerStatus sps);

    private enum ACLineStatus : byte
    {
      Offline = 0, 
      Online = 1, 
      Unknown = 255
    }

    private enum BatteryFlag : byte
    {
      High = 1,
      Low = 2,
      Critical = 4,
      Charging = 8,
      NoSystemBattery = 128,
      Unknown = 255
    }

    private struct SystemPowerStatus
    {
      public ACLineStatus LineStatus;
      public BatteryFlag flgBattery;
      public Byte BatteryLifePercent;
      public Byte Reserved1;
      public Int32 BatteryLifeTime;
      public Int32 BatteryFullLifeTime;
    }

    /// <summary>
    /// Returns true if a an AC Power Line is detected
    /// </summary>
    public static Boolean ACPowerPluggedIn()
    {
      SystemPowerStatus SPS = new SystemPowerStatus();
      GetSystemPowerStatus(out SPS);

      if (SPS.LineStatus == ACLineStatus.Online)
      {
          return true;
      }
      else
      {
          return false;
      }
    }

    /// <summary>
    /// Returns an integer representing the percent of battery charge remaining.
    /// </summary>
    public static Int32 BatteryCharge()
    {
      SystemPowerStatus SPS = new SystemPowerStatus();
      GetSystemPowerStatus(out SPS);

      return (Int32)SPS.BatteryLifePercent;
    }
}
```
