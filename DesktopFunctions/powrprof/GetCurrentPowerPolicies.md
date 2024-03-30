
## C# Signature:
```cs
[DllImport("powrprof.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool GetCurrentPowerPolicies(out GLOBAL_POWER_POLICY pGlobalPowerPolicy, 
     out POWER_POLICY pPowerPolicy);
```

## VB Signature:
```cs
Declare Function GetCurrentPowerPolicies Lib "powrprof.dll" (TODO) As TODO
```

## Sample Code:
```cs
GLOBAL_POWER_POLICY gpp = new GLOBAL_POWER_POLICY();
POWER_POLICY pp = new POWER_POLICY();
if (!GetCurrentPowerPolicies(out gpp, out pp))
{
     throw new Win32Exception(Marshal.GetLastWin32Error());
}
```
