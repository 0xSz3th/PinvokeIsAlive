
## C# Signature:
```cs
struct WTS_PROCESS_INFO
    {
        public int SessionID;
        public int ProcessID;
        //This is a pointer to string...
        public IntPtr ProcessName;
        public IntPtr UserSid;
    }
```

## VB Signature:
```cs
Private Structure WTS_PROCESS_INFO
    Dim SessionID As Int32
    Dim ProcessID As Int32
    Dim ProcessName As Int32    'This is a pointer to string...which is not right for 64 bits...
    Dim UserSid As Int32
    End Structure
```
