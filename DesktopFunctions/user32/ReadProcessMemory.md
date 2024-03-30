
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
   public static extern bool ReadProcessMemory(
   IntPtr hProcess, 
   IntPtr lpBaseAddress,
   byte[] lpBuffer, 
   Int32 nSize, 
   out IntPtr lpNumberOfBytesRead);
```

## VB Signature:
```cs
Private Declare Function ReadProcessMemory Lib "kernel32" (ByVal hProcess As Integer, ByVal lpBaseAddress As Integer, ByVal lpBuffer As Integer, ByVal nSize As Integer, ByRef lpNumberOfBytesWritten As Integer) As Integer
```
