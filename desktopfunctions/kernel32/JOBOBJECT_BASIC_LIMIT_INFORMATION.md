
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
  struct JOBOBJECT_BASIC_LIMIT_INFORMATION
  {
    public Int64 PerProcessUserTimeLimit;
    public Int64 PerJobUserTimeLimit;
    public JOBOBJECTLIMIT LimitFlags;
    public UIntPtr MinimumWorkingSetSize;
    public UIntPtr MaximumWorkingSetSize;
    public UInt32 ActiveProcessLimit;
    public Int64 Affinity;
    public UInt32 PriorityClass;
    public UInt32 SchedulingClass;
  }
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential)> _
  Structure JOBOBJECT_BASIC_LIMIT_INFORMATION
    Public PerProcessUserTimeLimit As Int64
    Public PerJobUserTimeLimit As Int64
    Public LimitFlags As JOBOBJECTLIMIT
    Public MinimumWorkingSetSize As UIntPtr
    Public MaximumWorkingSetSize As UIntPtr
    Public ActiveProcessLimit As UInt32
    Public Affinity As Int64
    Public PriorityClass As UInt32
    Public SchedulingClass As UInt32
  End Structure
```
