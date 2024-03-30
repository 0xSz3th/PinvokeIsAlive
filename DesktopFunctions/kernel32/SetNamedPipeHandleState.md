
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool SetNamedPipeHandleState(IntPtr hNamedPipe, IntPtr lpMode,
   IntPtr lpMaxCollectionCount, IntPtr lpCollectDataTimeout);
```

## Notes:
```cs
[DllImport("kernel32.dll")]
  static extern bool SetNamedPipeHandleState(SafeFileHandle hNamedPipe, IntPtr lpMode,
     IntPtr lpMaxCollectionCount, IntPtr lpCollectDataTimeout);
```

## VB.NET 2.0 Signature:
```cs
<DllImport("kernel32.dll")> _
Public Function SetNamedPipeHandleState( _
    ByVal hNamedPipe As SafeFileHandle, _
    ByRef lpMode As Integer, _
    ByVal lpMaxCollectionCount As Integer, _
    ByVal lpCollectDataTimeout As Integer) As Boolean
End Function
```
