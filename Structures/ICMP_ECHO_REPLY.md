
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct ICMP_ECHO_REPLY
{
  public Int32 Address;
  public Int32 Status;
  public Int32 RoundTripTime;
  public Int16 DataSize;
  public Int16 Reserved;
  public IntPtr Data;
  public IP_OPTION_INFORMATION Options;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)>
Public Structure ICMP_ECHO_REPLY
   Public Address As Int32
   Public Status As Int32
   Public RoundTripTime As Int32
   Public DataSize As Int16
   Public Reserved As Int16
   Public Data As IntPtr
   Public Options As IP_OPTION_INFORMATION
End Structure
```
