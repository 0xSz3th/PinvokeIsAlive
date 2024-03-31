
## C# Definition:
```cs
[ComImport]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
[Guid("000214f4-0000-0000-c000-000000000046")]
interface IContextMenu2 {
    [PreserveSig]
    int QueryContextMenu(IntPtr hMenu, uint indexMenu, int idCmdFirst, int idCmdLast, uint uFlags);

    [PreserveSig]
    void InvokeCommand(IntPtr pici);

    [PreserveSig]
    void GetCommandString(int idcmd, uint uflags, int reserved, StringBuilder commandstring, int cch);

    [PreserveSig]
    int HandleMenuMsg(uint uMsg, IntPtr wParam, IntPtr lParam);
}
```

## VB Definition:
```cs
<ComImport> _
<Guid("TODO")> _
'TODO: Insert <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _ if this doesn't derive from IDispatch
Interface IContextMenu2
   TODO
End Interface
```
