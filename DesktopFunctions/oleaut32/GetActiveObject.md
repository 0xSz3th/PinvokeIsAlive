
## C# Signature:
```cs
// Returns a raw HRESULT:
[DllImport("oleaut32.dll")]
static extern int GetActiveObject(ref Guid rclsid, IntPtr pvReserved,
   [MarshalAs(UnmanagedType.IUnknown)] out Object ppunk);

// Converts failure HRESULTs to exceptions:
[DllImport("oleaut32.dll", PreserveSig=false)]
static extern void GetActiveObject(ref Guid rclsid, IntPtr pvReserved,
   [MarshalAs(UnmanagedType.IUnknown)] out Object ppunk);
```

## VB Signature:
```cs
Declare Function GetActiveObject Lib "oleaut32.dll" ( _
   ByRef rclsid As Guid, pvReserved As IntPtr, _
   <MarshalAs(UnmanagedType.IUnknown), Out> ppunk As Object) As Integer
```
