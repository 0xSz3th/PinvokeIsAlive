
## C# Definition:
```cs
[StructLayoutAttribute(LayoutKind.Sequential)]
struct SECURITY_DESCRIPTOR {
   public byte revision;
   public byte size;
   public short control;
   public IntPtr owner;
   public IntPtr group;
   public IntPtr sacl;
   public IntPtr dacl;
}
```

## VB Definition:
```cs
<StructLayoutAttribute(LayoutKind.Sequential)> _
  Public Structure SECURITY_DESCRIPTOR
    Public revision As Byte
    Public size As Byte
    Public control As Short
    Public owner As IntPtr
    Public group As IntPtr
    Public sacl As IntPtr
    Public dacl As IntPtr
  End Structure
```
