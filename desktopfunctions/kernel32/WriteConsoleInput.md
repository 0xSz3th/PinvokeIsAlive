
## C# Signature:
```cs
/* Writes data directly to the console input buffer. */
    [DllImport("kernel32.dll", EntryPoint = "WriteConsoleInputW", CharSet = CharSet.Unicode, SetLastError = true)]
    internal static extern bool WriteConsoleInput(
        IntPtr hConsoleInput,
        INPUT_RECORD[] lpBuffer,
        uint nLength,
        out uint lpNumberOfEventsWritten);
```

## Sample Code:
```cs
[DllImport("kernel32")]
    public static extern IntPtr GetStdHandle(StdHandle index);

    public enum StdHandle
    {
    OutputHandle = -11,
    InputHandle = -10,
    ErrorHandle = -12
    }

    static void Main(string[] args)
    {
    INPUT_RECORD[] record = new INPUT_RECORD[1];

    record[0].EventType = INPUT_RECORD.KEY_EVENT;

    record[0].KeyEvent = new KEY_EVENT_RECORD();
    record[0].KeyEvent.UnicodeChar = 'a';
    record[0].KeyEvent.AsciiChar = (byte)'a';
    record[0].KeyEvent.bKeyDown = true;

    uint recordsWritten = 0;
    bool boi = WriteConsoleInput(GetStdHandle(StdHandle.InputHandle), record, 1, out recordsWritten);
    }
```
