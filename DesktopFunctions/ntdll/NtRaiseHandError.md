
## C# Signature:
```cs
[DllImport("ntdll.dll")]
    private static extern uint NtRaiseHardError(
    uint ErrorStatus, 
    uint NumberOfParameters, 
    uint UnicodeStringParameterMask, 
    IntPtr Parameters, 
    uint ValidResponseOption, 
    out uint Response
```

## or C# Signature (with NT-Status enum):
```cs
[DllImport("ntdll.dll")]
    private static extern uint NtRaiseHardError(
    NtStatus ErrorStatus, 
    uint NumberOfParameters, 
    uint UnicodeStringParameterMask, 
    IntPtr Parameters, 
    uint ValidResponseOption, 
    out uint Response
```

## VB Signature:
```cs
<DllImport("ntdll.dll")>
    Private Shared Function NtRaiseHardError(ByVal ErrorStatus As UInteger, ByVal NumberOfParameters As UInteger, ByVal UnicodeStringParameterMask As UInteger, ByVal Parameters As IntPtr, ByVal ValidResponseOption As UInteger, <Out()> ByRef Response As UInteger) As 
    UInteger
    End Function
```

## C# Sample Code:
```cs
Console.Write("Press any key to trigger a BSOD.");
    Console.ReadKey();
    RtlAdjustPrivilege(19, true, false, out bool previousValue);
    NtRaiseHandError(0xC0000420, 0, 0, IntPtr.Zero, 6, out uint Response);
```

## VB.Net Sample Code:
```cs
Console.Write("Press any key to trigger a BSOD.")
    Console.ReadKey()
    Dim previousValue As Boolean
    RtlAdjustPrivilege(19, True, False, previousValue)
    Dim Response As UInteger
    NtRaiseHardError(3221226528, 0, 0, IntPtr.Zero, 6, Response)
Return Type is NTSTATUS but too long type definition to wrote this page2/9/2023 12:37:01 PM - -103.186.185.230
```
