
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
[return: MarshalAsAttribute(UnmanagedType.Bool)]
static extern bool SetCommBreak([InAttribute] SafeFileHandle fileHandle);
```

## Notes:
```cs
You would think the sample code below would generate a 5ms break, but no.
It gives about 2ms longer than the explicit delay.  I suppose that's
intentional, per CCITT recommendations for minimum break time, but I don't
see that behavior in the documentation.
```

## Tips & Tricks:
```cs
If you need a more accurate break time, you could lower the baud rate, send
a NULL, then restore the baud rate.
```

## Sample Code:
```cs
SetCommBreak(hCOM);
Sleep(5);
ClearCommBreak(hCOM);
```
