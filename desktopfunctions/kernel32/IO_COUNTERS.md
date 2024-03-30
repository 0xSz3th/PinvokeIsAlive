
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
  struct IO_COUNTERS
  {
    public UInt64 ReadOperationCount;
    public UInt64 WriteOperationCount;
    public UInt64 OtherOperationCount;
    public UInt64 ReadTransferCount;
    public UInt64 WriteTransferCount;
    public UInt64 OtherTransferCount;
  }
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential)> _
  Structure IO_COUNTERS
    Public ReadOperationCount As UInt64
    Public WriteOperationCount As UInt64
    Public OtherOperationCount As UInt64
    Public ReadTransferCount As UInt64
    Public WriteTransferCount As UInt64
    Public OtherTransferCount As UInt64
  End Structure
```
