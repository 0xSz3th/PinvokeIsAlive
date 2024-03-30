
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool DefineDosDevice(uint dwFlags, string lpDeviceName,
   string lpTargetPath);
```

## Sample Code:
```cs
// Define a virtual drive
VolumeFunctions.DefineDosDevice(0, @"Y:", @"c:\test\folder\name\");

// Delete a virtual drive. The drive letter and folder must match.
VolumeFunctions.DefineDosDevice(
    VolumeFunctions.DDD_REMOVE_DEFINITION + VolumeFunctions.DDD_EXACT_MATCH_ON_REMOVE, 
    @"Y:", 
    @"C:\test\folder\name");

// Delete if you know only the drive letter.
DeleteVolumeMountPoint(@"Y:\");
```

## Sample Code:
```cs
public class VolumeFunctions
{
    [DllImport("kernel32.dll")]
    internal static extern bool DefineDosDevice(uint dwFlags, string lpDeviceName,
    string lpTargetPath);

    [DllImport("Kernel32.dll")]
    internal static extern uint QueryDosDevice(string lpDeviceName,
    string lpTargetPath,uint ucchMax);

    internal const uint DDD_RAW_TARGET_PATH = 0x00000001;
    internal const uint DDD_REMOVE_DEFINITION = 0x00000002;
    internal const uint DDD_EXACT_MATCH_ON_REMOVE = 0x00000004;
    internal const uint DDD_NO_BROADCAST_SYSTEM = 0x00000008; 
}
```
