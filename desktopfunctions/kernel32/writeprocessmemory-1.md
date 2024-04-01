# WriteProcessMemory

### C# Definition:



```csharp
[DllImport("kernel32.dll", SetLastError = true)]
        public static extern bool WriteProcessMemory(
          IntPtr hProcess,
          IntPtr lpBaseAddress,
          IntPtr lpBuffer,
          Int32 nSize,
          out IntPtr lpNumberOfBytesWritten);
```
