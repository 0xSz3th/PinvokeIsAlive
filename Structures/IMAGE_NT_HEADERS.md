
## C# Definition:
```cs
[StructLayout(LayoutKind.Explicit)]
    public struct IMAGE_NT_HEADERS32
    {
        [FieldOffset(0)]
        public UInt32 Signature;

        [FieldOffset(4)]
        public IMAGE_FILE_HEADER FileHeader;

        [FieldOffset(24)]
        public IMAGE_OPTIONAL_HEADER32 OptionalHeader;

        private string _Signature
        {
        get { return new string(Signature); }
        }

        public bool isValid
        {
        get { return _Signature == "PE\0\0" && OptionalHeader.Magic == MagicType.IMAGE_NT_OPTIONAL_HDR32_MAGIC; }
        }
    }
    [StructLayout(LayoutKind.Explicit)]
    public struct IMAGE_NT_HEADERS64
    {
        [FieldOffset(0)]
        public UInt32 Signature;

        [FieldOffset(4)]
        public IMAGE_FILE_HEADER FileHeader;

        [FieldOffset(24)]
        public IMAGE_OPTIONAL_HEADER64 OptionalHeader;

        private string _Signature
        {
        get { return new string(Signature); }
        }

        public bool isValid
        {
        get { return _Signature == "PE\0\0" && OptionalHeader.Magic == MagicType.IMAGE_NT_OPTIONAL_HDR64_MAGIC; }
        }
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Public Structure IMAGE_NT_HEADERS32
        Public Signature As UInt32
        Public FileHeader As IMAGE_FILE_HEADER
        Public OptionalHeader As IMAGE_OPTIONAL_HEADER32
    End Structure

    <StructLayout(LayoutKind.Sequential)> _
    Public Structure IMAGE_NT_HEADERS64
        Public Signature As UInt32
        Public FileHeader As IMAGE_FILE_HEADER
        Public OptionalHeader As IMAGE_OPTIONAL_HEADER64
    End Structure
```

##  VB6 Definition:
```cs
Public Type IMAGE_NT_HEADERS32
        Signature As Long
        FileHeader As IMAGE_FILE_HEADER
        OptionalHeader As IMAGE_OPTIONAL_HEADER32
    End Type

    Public Type IMAGE_NT_HEADERS64
        Signature As Long
        FileHeader As IMAGE_FILE_HEADER
        OptionalHeader As IMAGE_OPTIONAL_HEADER64
    End Type
```
