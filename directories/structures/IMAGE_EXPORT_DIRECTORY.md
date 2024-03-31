
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct IMAGE_EXPORT_DIRECTORY
    {
        public UInt32 Characteristics;
        public UInt32 TimeDateStamp;
        public UInt16 MajorVersion;
        public UInt16 MinorVersion;
        public UInt32 Name;
        public UInt32 Base;
        public UInt32 NumberOfFunctions;
        public UInt32 NumberOfNames;
        public UInt32 AddressOfFunctions;     // RVA from base of image
        public UInt32 AddressOfNames;     // RVA from base of image
        public UInt32 AddressOfNameOrdinals;  // RVA from base of image
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Public Structure IMAGE_EXPORT_DIRECTORY
    Public Characteristics As Integer
    Public TimeDateStamp As Integer
    Public MajorVersion As Short
    Public MinorVersion As Short
    Public Name As Integer
    Public Base As Integer
    Public NumberOfFunctions As Integer
    Public NumberOfNames As Integer
    Public AddressOfFunctions As Integer
    Public AddressOfNames As Integer
    Public AddressOfNameOrdinals As Integer
    End Structure
```
