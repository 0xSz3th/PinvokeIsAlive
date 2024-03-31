# PROCESS\_INFORMATION

### C# Definition:

```csharp
[StructLayout(LayoutKind.Sequential)]
        internal struct PROCESS_INFORMATION
        {
          public IntPtr hProcess;
          public IntPtr hThread;
          public int dwProcessId;
          public int dwThreadId;
        }
```
