
## C# Signature:
```cs
/// <summary>
/// Sets the last-error code for the calling thread.
/// </summary>
/// <param name="dwErrorCode">The last-error code for the thread.</param>
[DllImport("kernel32.dll", SetLastError = true)]
static extern void SetLastError(uint dwErrorCode);
```

## VB.NET Signature:
```cs
Declare Function SetLastError Lib "kernel32.dll" (ByVal dwErrCode As Integer) As Integer
```
