
## C# Signature:
```cs
[SuppressMessage("Microsoft.Security", "CA2118:ReviewSuppressUnmanagedCodeSecurityUsage")]
    [DllImport(ExternDll.Kernel32, SetLastError=true, ExactSpelling=true, EntryPoint="RtlMoveMemory", CharSet=System.Runtime.InteropServices.CharSet.Auto)]
    [ResourceExposure(ResourceScope.None)]
    public static extern void CopyMemory(HandleRef destData, HandleRef srcData, int size);
```

## VB Signature:
```cs
<SuppressMessage("Microsoft.Security", "CA2118:ReviewSuppressUnmanagedCodeSecurityUsage")>
    <DllImport("Ntdll.dll", SetLastError:=True, ExactSpelling:=True, EntryPoint:="RtlMoveMemory", CharSet:=System.Runtime.InteropServices.CharSet.Auto)>
    Public Shared Sub CopyMemory(ByVal destData As HandleRef, ByVal srcData As HandleRef, ByVal size As Integer)

    End Sub
```
