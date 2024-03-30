
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 mixerOpen(ref IntPtr phmx, uint pMxId,
   IntPtr dwCallback, IntPtr dwInstance, UInt32 fdwOpen);
```

## VB Signature:
```cs
Declare Function mixerOpen Lib "winmm.dll" (ByRef phmx As IntPtr, ByVal pMxId As UInteger, ByVal dwCallback As IntPtr, ByVal dwInstance As IntPtr, ByVal fdwOpen As UInteger) As Integer
```
