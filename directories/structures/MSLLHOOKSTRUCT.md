
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct MSLLHOOKSTRUCT
{
    public POINT pt;
    public int mouseData; // be careful, this must be ints, not uints (was wrong before I changed it...). regards, cmew.
    public int flags;
    public int time;
    public UIntPtr dwExtraInfo;
}
```

## VB.NET Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure MSLLHOOKSTRUCT
    Public pt As POINT
    Public mouseData As Int32
    Public flags As MSLLHOOKSTRUCTFlags
    Public time As Int32
    Public dwExtraInfo As UIntPtr
End Structure

<Flags()> _
Public Enum MSLLHOOKSTRUCTFlags As Int32
    LLMHF_INJECTED = 1
End Enum
```
