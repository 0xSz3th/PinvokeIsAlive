
## C# Signature:
```cs
// uint output
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool GetExitCodeThread(IntPtr hThread, out uint lpExitCode);

// IntPtr output
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool GetExitCodeThread(IntPtr hThread, IntPtr lpExitCode);
```

## VB Signature:
```cs
' UInteger output
Declare Function GetExitCodeThread Lib "kernel32.dll" (ByVal hThread As IntPtr, ByRef lpExitCode As UInteger) As Boolean

' IntPtr output
Declare Function GetExitCodeThread Lib "kernel32.dll" (ByVal hThread As IntPtr, ByVal lpExitCode As IntPtr) As Boolean
```

## Sample Code:
```cs
uint dwOut = 0;
while (GetExitCodeThread(hThread, out dwOut))
{
     if (dwOut != 0x103)
     break;

     Thread.Sleep(10); // Don't cook our CPU
}

Console.WriteLine("Thread exit code: {0}", dwOut);
```
