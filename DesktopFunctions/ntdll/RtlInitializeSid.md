
## C# Signature:
```cs
[DllImport("ntdll", CharSet = CharSet.Auto, ExactSpelling = true, SetLastError = true)]
private static extern Int32 RtlInitializeSid([In, Out] ref SID Sid, [In] ref SID_IDENTIFIER_AUTHORITY IdentifierAuthority, byte SubAuthorityCount);
```

## VB Signature:
```cs
Declare Function RtlInitializeSid Lib "ntdll.dll" (TODO) As TODO
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, Size = 6)]
struct SID_IDENTIFIER_AUTHORITY
{
   [MarshalAs(UnmanagedType.ByValArray, SizeConst = 6)]
   public byte[] Value;

   public SID_IDENTIFIER_AUTHORITY(byte[] value)
   {
     if (value.Length != 6)
       throw new ArgumentOutOfRangeException("value", "Value must be an array of 6 bytes.");
     this.Value = value;
   }
}

[StructLayout(LayoutKind.Sequential)]
struct SID
{
   public byte Revision;
   public byte SubAuthorityCount;
   public SID_IDENTIFIER_AUTHORITY IdentifierAuthority;
   public UInt32[] SubAuthority;

   public SID(int subAuthorityCount)
   {
     this.Revision = 0;
     this.SubAuthorityCount = 0;
     this.IdentifierAuthority = default(SID_IDENTIFIER_AUTHORITY);
     this.SubAuthority = new UInt32[subAuthorityCount];
   }
}
```

## Sample Code:
```cs
// just using a null identifier here
SID_IDENTIFIER_AUTHORITY id = new SID_IDENTIFIER_AUTHORITY(new byte[] { 0, 0, 0, 0, 0, 0 });
// new SID with an allocated SubAuthority count of 1
SID sid = new SID(1);

// make the call, passing the correct SubAuthority count
var status = RtlInitializeSid(ref sid, ref id, (byte)sid.SubAuthority.Length);

if (status < 0)
   Console.WriteLine("Failed.");
else
   Console.WriteLine("Success.");
```
