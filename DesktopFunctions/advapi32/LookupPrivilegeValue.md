
## C# Signature:
```cs
[DllImport("advapi32.dll")]
static extern bool LookupPrivilegeValue(string lpSystemName, string lpName,
   ref LUID lpLuid);
```

## VB Signature:
```cs
Declare Function LookupPrivilegeValue Lib "advapi32.dll" (lpSystemName As String, _
   lpName As String, ByRef lpLuid As LUID) As Boolean
```

## Sample Code:
```cs
[DllImport("advapi32.dll")]
        public static extern bool LookupPrivilegeValue(string systemName, string privilegeName, ref LUID luid);

        public static bool LookupPrivilegeValue(string systemName, PrivilegeNames privilegeName, ref LUID luid)
        {
            return LookupPrivilegeValue(systemName, privilegeName.ToString(), ref luid);
        }

        public static LUID LookupPrivilegeValue(string systemName, PrivilegeNames privilegeName)
        {
            var luid = new LUID();
            return LookupPrivilegeValue(systemName, privilegeName, ref luid) ? luid : new LUID();
        }
```
