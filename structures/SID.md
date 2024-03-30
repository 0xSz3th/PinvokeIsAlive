
## C# Definition:
```cs
struct SID_IDENTIFIER_AUTHORITY 
{
   [MarshalAs(UnmanagedType.ByValArray, SizeConst=6)]
   public byte[] Value;

   public SID_IDENTIFIER_AUTHORITY(byte[] value)
   {
       Value = value;
   }
}
```

## VB Definition:
```cs
Structure SID_IDENTIFIER_AUTHORITY
    <MarshalAs(UnmanagedType.ByValArray, SizeConst:=6)> _
    Public Value() As Byte

    Public Sub New(ByVal val As Byte())
      Value = val
    End Sub
  End Structure
```
