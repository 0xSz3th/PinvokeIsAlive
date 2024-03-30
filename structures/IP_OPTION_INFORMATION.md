
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct IP_OPTION_INFORMATION
{
  public byte TimeToLive;
  public byte TypeOfService;
  public byte Flags;
  public byte OptionsSize;
  public IntPtr OptionsData;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)>
Public Structure IP_OPTION_INFORMATION
   Public TimeToLive As Byte
   Public TypeOfService As Byte
   Public Flags As Byte
   Public OptionsSize As Byte
   Public OptionsData As IntPtr
End Structure
```
