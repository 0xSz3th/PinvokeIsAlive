
## C# Signature:
```cs
[DllImport("shell32.dll", SetLastError=true, EntryPoint="#2", CharSet=CharSet.Auto)]
static extern UInt32 SHChangeNotifyRegister(
            IntPtr hWnd,
            SHCNF fSources,
            SHCNE fEvents,
            uint wMsg,
            int cEntries,
            ref SHChangeNotifyEntry pFsne);
```

## C# Signature:
```cs
[DllImport("shell32.dll", EntryPoint = "#2", CharSet = CharSet.Auto)]
static extern uint SHChangeNotifyRegister(
            IntPtr hWnd,
            SHCNRF fSources,
            SHCNE fEvents,
            uint wMsg,
            int cEntries,
            [MarshalAs(UnmanagedType.LPArray)] SHChangeNotifyEntry[] pFsne);
```

## VB Signature:
```cs
Declare Function SHChangeNotifyRegister Lib "shell32.dll" (TODO) As TODO
```
