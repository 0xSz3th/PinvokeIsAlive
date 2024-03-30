
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern uint SHFormatDrive(IntPtr hwnd, uint drive, uint fmtID,
   uint options);
```

## User-Defined Types:
```cs
public enum SHFormatFlags : uint {
     SHFMT_ID_DEFAULT = 0xFFFF,
     SHFMT_OPT_FULL = 0x1,
     SHFMT_OPT_SYSONLY = 0x2,
     SHFMT_ERROR = 0xFFFFFFFF,
     SHFMT_CANCEL = 0xFFFFFFFE,
     SHFMT_NOFORMAT = 0xFFFFFFD,
}
```

## Another C# Signature:
```cs
[DllImport("shell32.dll")]
static extern uint SHFormatDrive(IntPtr hwnd, uint drive, SHFormatFlags fmtID,
                       SHFormatOptions options);
```

## User-Defined Types:
```cs
public enum SHFormatFlags : uint
{
     SHFMT_ID_DEFAULT = 0xFFFF,
}

[Flags]
public enum SHFormatOptions : uint
{
     SHFMT_OPT_FULL = 0x1,
     SHFMT_OPT_SYSONLY = 0x2,
}
```

## User-Defined Helper Method:
```cs
public const uint SHFMT_ERROR       = 0xFFFFFFFF;
public const uint SHFMT_CANCEL      = 0xFFFFFFFE;
public const uint SHFMT_NOFORMAT    = 0xFFFFFFD;

/// <summary>
/// Permit to check the result of the format call
/// Throw Exception with a detailed message
/// </summary>
/// <param name="shFormatResult"></param>
public static void CheckFormatResult(uint shFormatResult)
{
     if (shFormatResult == SHFMT_ERROR)
     throw new Exception("An error occurred during the format. This does not indicate that the drive is unformattable.");
     if (shFormatResult == SHFMT_CANCEL)
     throw new OperationCanceledException("The format was canceled.");
     if (shFormatResult == SHFMT_NOFORMAT)
     throw new IOException("The drive cannot be formatted.");

     //we can exit normally
     return;
}
```

## Converting a DriveInfo to drive number in C#:
```cs
DriveInfo drive = new DriveInfo("F:\\");
byte[] bytes = Encoding.ASCII.GetBytes(drive.Name.ToCharArray());
uint driveNumber = Convert.ToUInt32(bytes[0] - Encoding.ASCII.GetBytes(new [] {'A'})[0]);
```

## Sample Code:
```cs
uint result = SHFormatDrive( this.Handle, 
              2, // formatting C:
              (uint)SHFormatFlags.SHFMT_ID_DEFAULT,
              0 ); // full format of C:
if ( result == SHFormatFlags.SHFMT_ERROR ) 
    MessageBox.Show( "Unable to format the drive" );
```

## Sample Code:
```cs
SHFormatDrive( IntPtr.Zero, 
              2, // formatting C:
              (uint)SHFormatFlags.SHFMT_ID_DEFAULT,
              0 ); // full format of C:
```

## Another Sample Code:
```cs
byte[] bytes = Encoding.ASCII.GetBytes(drive.Name.ToCharArray());
uint driveNumber = Convert.ToUInt32(bytes[0] - Encoding.ASCII.GetBytes(new [] {'A'})[0]);

uint shFormatResult = SHFormatDrive(IntPtr.Zero, driveNumber, SHFormatFlags.SHFMT_ID_DEFAULT, SHFormatOptions.SHFMT_OPT_FULL);
CheckFormatResult(shFormatResult);
```
