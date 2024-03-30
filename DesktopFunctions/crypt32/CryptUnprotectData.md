
## C# Signature:
```cs
[
DllImport("Crypt32.dll",
SetLastError=true, 
CharSet=System.Runtime.InteropServices.CharSet.Auto)
]
[return: MarshalAs(UnmanagedType.Bool)]
private static extern bool CryptUnprotectData(
    ref DATA_BLOB pDataIn, 
    StringBuilder szDataDescr, 
    ref DATA_BLOB pOptionalEntropy, 
    IntPtr pvReserved, 
    ref CRYPTPROTECT_PROMPTSTRUCT pPromptStruct, 
    CryptProtectFlags dwFlags, 
    ref DATA_BLOB pDataOut
);
```

## VB .NET Signature:
```cs
<DllImport("Crypt32.dll", SetLastError:=True, CharSet:=System.Runtime.InteropServices.CharSet.Auto)> _
Private Shared Function CryptUnprotectData _
( _
     ByRef pDataIn As DATA_BLOB, _
     ByVal szDataDescr As StringBuilder, _
     ByRef pOptionalEntropy As DATA_BLOB, _
     ByVal pvReserved As IntPtr, _
     ByRef pPromptStruct As CRYPTPROTECT_PROMPTSTRUCT, _
     ByVal dwFlags As Integer, _
     ByRef pDataOut As DATA_BLOB _
) As Boolean
End Function
```
