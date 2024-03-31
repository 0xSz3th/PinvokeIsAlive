
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct MSGBOXPARAMS
{    
    public uint cbSize; 
    public IntPtr hwndOwner; 
    public IntPtr hInstance;
    public String lpszText; 
    public String lpszCaption; 
    public uint dwStyle;
    public IntPtr lpszIcon;
    public IntPtr dwContextHelpId; 
    public MsgBoxCallback lpfnMsgBoxCallback; 
    public uint dwLanguageId;
}
```

## VB Definition:
```cs
TODO
```

## User-Defined Field Types:
```cs
// Delegate declaration for a callback that gets called when the help button on the message box is pushed.
public delegate void MsgBoxCallback( [HELPINFO] lpHelpInfo );
```

## Notes:
```cs
None.
```
