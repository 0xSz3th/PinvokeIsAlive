
## C# Signature:
```cs
[DllImport("advapi32.dll", SetLastError = true, CharSet = CharSet.Unicode)]
    static extern bool ConvertSecurityDescriptorToStringSecurityDescriptor(
        IntPtr SecurityDescriptor, 
        uint StringSDRevision, 
        SECURITY_INFORMATION SecurityInformation, 
        out IntPtr StringSecurityDescriptor, 
        out uint StringSecurityDescriptorSize);
```

## VB Signature:
```cs
Declare Unicode Function ConvertSecurityDescriptorToStringSecurityDescriptor Lib "advapi32.dll" Alias "ConvertSecurityDescriptorToStringSecurityDescriptorW" (SD As IntPtr, SDRevision As Integer, SecurityInfo As SECURITY_INFORMATION, ByRef StringSD As IntPtr, StringSDLength As IntPtr) As Boolean
```
