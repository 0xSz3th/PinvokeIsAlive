
## C# Signature:
```cs
[DllImport("netapi32.dll", SetLastError=true)]
static extern UInt32 NetShareSetInfo(String servername, String netname, UInt32 level, ref object buf, out UInt32 parm_err);
```

## VB Signature:
```cs
Declare Function NetShareSetInfo Lib "netapi32.dll" (TODO) As TODO
```
