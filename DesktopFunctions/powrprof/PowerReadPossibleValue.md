
## C# Signature:
```cs
[DllImport("PowrProf.dll", SetLastError=true)]
public static extern uint PowerReadPossibleValue(IntPtr RootPowerKey, IntPtr SubGroupOfPowerSettingGuid, IntPtr PowerSettingGuid, ref RegType Type, UInt32 PossibleSettingIndex, IntPtr Buffer, ref UInt32 BufferSize);
```

## VB Signature:
```cs
Declare Function PowerReadPossibleValue Lib "powrprof.dll" (TODO) As TODO
```
