
## C# Definition:
```cs
[ComImport]
[Guid("00000139-0000-0000-c000-000000000046")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
interface IEnumSTATPROPSTG
{
    int Next(int count,
        [MarshalAs(UnmanagedType.LPArray, SizeParamIndex = 0), Out]
        STATPROPSTG[] elements);

    void Skip(int count);

    void Reset();

    [return: MarshalAs(UnmanagedType.Interface)]
    IEnumSTATPROPSTG Clone();
}
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
internal struct STATPROPSTG
{
    [MarshalAs(UnmanagedType.LPWStr)]
    public string lpwstrName;
    public uint propid;
    public ushort vt;

}
```
