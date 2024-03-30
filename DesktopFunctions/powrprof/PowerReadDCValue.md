
## C# Signature:
```cs
[DllImport("PowrProf.dll", SetLastError=true)]
public static extern uint PowerReadDCValue(IntPtr RootPowerKey, IntPtr SchemeGuid, IntPtr SubGroupOfPowerSettingGuid, IntPtr PowerSettingGuid, ref RegType Type, IntPtr Buffer, ref UInt32 BufferSize);
```

## VB Signature:
```cs
Declare Function PowerReadDCValue Lib "powrprof.dll" (TODO) As TODO
```
