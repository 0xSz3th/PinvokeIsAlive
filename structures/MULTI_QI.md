
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
struct MULTI_QI
{
    [MarshalAs(UnmanagedType.LPStruct)]  public Guid pIID;
    [MarshalAs(UnmanagedType.Interface)] public object pItf;
    public int hr;
}
```
