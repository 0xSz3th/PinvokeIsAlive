
## C# Signature:
```cs
[ComImport(), 
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown), 
    GuidAttribute("000214e4-0000-0000-c000-000000000046")]
    public interface IContextMenu
    {
        [PreserveSig()]
        int QueryContextMenu(
            uint hMenu, 
            uint indexMenu, 
            int idCmdFirst, 
            int idCmdLast, 
            uint uFlags);

        [PreserveSig()]
        void InvokeCommand(IntPtr pici);

        [PreserveSig()]
        void GetCommandString(
            int idcmd, 
            uint uflags, 
            int reserved, 
            StringBuilder commandstring, 
            int cch);
    }
```

## VB Signature:
```cs
<ComImport()> _
<InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
<GuidAttribute("000214e4-0000-0000-c000-000000000046")> _
Public Interface IContextMenu
     <PreserveSig()> _
     Function QueryContextMenu( _
     ByVal hMenu As Integer, _
     ByVal indexMenu As Integer, _
     ByVal idCmdFirst As Integer, _
     ByVal idCmdLast As Integer, _
     ByVal uFlags As Integer) As Integer

     <PreserveSig()> _
     Sub InvokeCommand(ByVal pici As IntPtr)

     <PreserveSig()> _
     Sub GetCommandString( _
     ByVal idcmd As Integer, _
     ByVal uflags As Integer, _
     ByVal reserved As Integer, _
     ByVal commandstring As StringBuilder, _
     ByVal cch As Integer)
End Interface
```

## Sample Code:
```cs
string commandStr = "" ;
    if ((uFlags & (uint)GCS.VERB) != 0) 
    {
        //obviously you could insert some cases here
        switch (idCmd)
        {
            default:
                commandStr = "..."; 
                break;
        }
    }
    if((uFlags  & (uint)GCS.HELPTEXT) != 0)
    {
        switch (idCmd)
        {
            case 0:
                commandStr = "Menu Item 1. And a brief description of what it does.";
                break;
            case 1:
                commandStr = "Menu Item 2. And a brief description of what it does." ;
                break;
            case 2:
                commandStr = "Menu Item 3. And a brief description of what it does.";
                break;
            case 3:
                commandStr = "Menu Item 4. And a brief description of what it does."; 
                break;
            default:
                commandStr = "..."; 
                break;
        }
    }

    // must limit the return string to cchMax
    if (commandStr.Length >= cchMax) commandStr = commandStr.Substring(0, cchMax-1) ;

    // now return unicode or ansi based on uFlags
    if((uFlags  & (uint)GCS.UNICODE) != 0 ) 
    {
        str = Marshal.StringToHGlobalUni(commandStr);
        Helpers.lstrcpynW(commandString, str, cchMax);
        Marshal.FreeHGlobal(str);
    }
    else 
    {
        str = Marshal.StringToHGlobalAnsi(commandStr);
        Helpers.lstrcpynA(commandString, str, cchMax);
        Marshal.FreeHGlobal(str);
    }
```
