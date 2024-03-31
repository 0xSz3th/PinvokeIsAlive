
## C# Definition:
```cs
private struct PROCESS_BASIC_INFORMATION
{
  public NtStatus ExitStatus;
  public IntPtr PebBaseAddress;
  public UIntPtr AffinityMask;
  public int BasePriority;
  public UIntPtr UniqueProcessId;
  public UIntPtr InheritedFromUniqueProcessId;
}
```

## C# Alternate Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
internal struct PROCESS_BASIC_INFORMATION
{
    public IntPtr ExitStatus;
    public IntPtr PebAddress;
    public IntPtr AffinityMask;
    public IntPtr BasePriority;
    public IntPtr UniquePID;
    public IntPtr InheritedFromUniqueProcessId;
}
```

## C# Alt Alt Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
internal struct PROCESS_BASIC_INFORMATION
{
    public IntPtr Reserved1;
    public IntPtr PebAddress;
    public IntPtr Reserved2;
    public IntPtr Reserved3;
    public IntPtr UniquePid;
    public IntPtr MoreReserved;
}
```

## VB.NET Definition:
```cs
Private Structure PROCESS_BASIC_INFORMATION
    Public ExitStatus As NtStatus
    Public PebBaseAddress As IntPtr
    Public AffinityMask As UIntPtr
    Public BasePriority As Integer
    Public UniqueProcessId As UIntPtr
    Public InheritedFromUniqueProcessId As UIntPtr
End Structure
```
