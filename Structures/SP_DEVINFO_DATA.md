
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct SP_DEVINFO_DATA
{
   public UInt32 cbSize;
   public Guid ClassGuid;
   public UInt32 DevInst;
   public IntPtr Reserved;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Private Structure SP_DEVINFO_DATA
    Public cbSize As Integer
    Public ClassGuid As Guid
    Public PropertyID As Integer
    Public Reserved As IntPtr
    End Structure
```
