
## C# Definitions:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct STGMEDIUM
{
    [MarshalAs(UnmanagedType.U4)]
    public int tymed;
    public IntPtr data;
    [MarshalAs(UnmanagedType.IUnknown)]
    public object pUnkForRelease;
}

[ComVisibleAttribute(false)]
[StructLayoutAttribute(LayoutKind.Sequential)]
public class STGMEDIUM
{
    [MarshalAs(UnmanagedType.I4)]
    public int tymed;
    public IntPtr unionmember;
    public IntPtr pUnkForRelease;

}
```
