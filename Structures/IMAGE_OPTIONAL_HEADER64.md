
## C# Definition:
```cs
[StructLayout(LayoutKind.Explicit)]
public struct IMAGE_OPTIONAL_HEADER64
{
    [FieldOffset(0)]
    public MagicType Magic;

    [FieldOffset(2)]
    public byte MajorLinkerVersion;

    [FieldOffset(3)]
    public byte MinorLinkerVersion;

    [FieldOffset(4)]
    public uint SizeOfCode;

    [FieldOffset(8)]
    public uint SizeOfInitializedData;

    [FieldOffset(12)]
    public uint SizeOfUninitializedData;

    [FieldOffset(16)]
    public uint AddressOfEntryPoint;

    [FieldOffset(20)]
    public uint BaseOfCode;

    [FieldOffset(24)]
    public ulong ImageBase;

    [FieldOffset(32)]
    public uint SectionAlignment;

    [FieldOffset(36)]
    public uint FileAlignment;

    [FieldOffset(40)]
    public ushort MajorOperatingSystemVersion;

    [FieldOffset(42)]
    public ushort MinorOperatingSystemVersion;

    [FieldOffset(44)]
    public ushort MajorImageVersion;

    [FieldOffset(46)]
    public ushort MinorImageVersion;

    [FieldOffset(48)]
    public ushort MajorSubsystemVersion;

    [FieldOffset(50)]
    public ushort MinorSubsystemVersion;

    [FieldOffset(52)]
    public uint Win32VersionValue;

    [FieldOffset(56)]
    public uint SizeOfImage;

    [FieldOffset(60)]
    public uint SizeOfHeaders;

    [FieldOffset(64)]
    public uint CheckSum;

    [FieldOffset(68)]
    public SubSystemType Subsystem;

    [FieldOffset(70)]
    public DllCharacteristicsType DllCharacteristics;

    [FieldOffset(72)]
    public ulong SizeOfStackReserve;

    [FieldOffset(80)]
    public ulong SizeOfStackCommit;

    [FieldOffset(88)]
    public ulong SizeOfHeapReserve;

    [FieldOffset(96)]
    public ulong SizeOfHeapCommit;

    [FieldOffset(104)]
    public uint LoaderFlags;

    [FieldOffset(108)]
    public uint NumberOfRvaAndSizes;

    [FieldOffset(112)]
    public IMAGE_DATA_DIRECTORY ExportTable;

    [FieldOffset(120)]
    public IMAGE_DATA_DIRECTORY ImportTable;

    [FieldOffset(128)]
    public IMAGE_DATA_DIRECTORY ResourceTable;

    [FieldOffset(136)]
    public IMAGE_DATA_DIRECTORY ExceptionTable;

    [FieldOffset(144)]
    public IMAGE_DATA_DIRECTORY CertificateTable;

    [FieldOffset(152)]
    public IMAGE_DATA_DIRECTORY BaseRelocationTable;

    [FieldOffset(160)]
    public IMAGE_DATA_DIRECTORY Debug;

    [FieldOffset(168)]
    public IMAGE_DATA_DIRECTORY Architecture;

    [FieldOffset(176)]
    public IMAGE_DATA_DIRECTORY GlobalPtr;

    [FieldOffset(184)]
    public IMAGE_DATA_DIRECTORY TLSTable;

    [FieldOffset(192)]
    public IMAGE_DATA_DIRECTORY LoadConfigTable;

    [FieldOffset(200)]
    public IMAGE_DATA_DIRECTORY BoundImport;

    [FieldOffset(208)]
    public IMAGE_DATA_DIRECTORY IAT;

    [FieldOffset(216)]
    public IMAGE_DATA_DIRECTORY DelayImportDescriptor;

    [FieldOffset(224)]
    public IMAGE_DATA_DIRECTORY CLRRuntimeHeader;

    [FieldOffset(232)]
    public IMAGE_DATA_DIRECTORY Reserved;
}
```

## User-Defined Field Types:
```cs
public enum MachineType : ushort
{
    /// <summary>
    /// The content of this field is assumed to be applicable to any machine type
    /// </summary>
    Unknown = 0x0000,
    /// <summary>
    /// Intel 386 or later processors and compatible processors
    /// </summary>
    I386 = 0x014c,
    R3000 = 0x0162,
    /// <summary>
    ///  MIPS little endian
    /// </summary>
    R4000 = 0x0166,
    R10000 = 0x0168,
    /// <summary>
    /// MIPS little-endian WCE v2
    /// </summary>
    WCEMIPSV2 = 0x0169,
    /// <summary>
    /// Alpha AXP
    /// </summary>
    Alpha = 0x0184,
    /// <summary>
    /// Hitachi SH3
    /// </summary>
    SH3 = 0x01a2,
    /// <summary>
    /// Hitachi SH3 DSP
    /// </summary>
    SH3DSP = 0x01a3,
    /// <summary>
    /// Hitachi SH4
    /// </summary>
    SH4 = 0x01a6,
    /// <summary>
    /// Hitachi SH5
    /// </summary>
    SH5 = 0x01a8,
    /// <summary>
    /// ARM little endian
    /// </summary>
    ARM = 0x01c0,
    /// <summary>
    /// Thumb
    /// </summary>
    Thumb = 0x01c2,
    /// <summary>
    /// ARM Thumb-2 little endian
    /// </summary>
    ARMNT = 0x01c4,
    /// <summary>
    /// Matsushita AM33
    /// </summary>
    AM33 = 0x01d3,
    /// <summary>
    /// Power PC little endian
    /// </summary>
    PowerPC = 0x01f0,
    /// <summary>
    /// Power PC with floating point support
    /// </summary>
    PowerPCFP = 0x01f1,
    /// <summary>
    /// Intel Itanium processor family
    /// </summary>
    IA64 = 0x0200,
    /// <summary>
    /// MIPS16
    /// </summary>
    MIPS16 = 0x0266,
    /// <summary>
    /// Motorola 68000 series
    /// </summary>
    M68K = 0x0268,
    /// <summary>
    /// Alpha AXP 64-bit
    /// </summary>
    Alpha64 = 0x0284,
    /// <summary>
    /// MIPS with FPU
    /// </summary>
    MIPSFPU = 0x0366,
    /// <summary>
    /// MIPS16 with FPU
    /// </summary>
    MIPSFPU16 = 0x0466,
    /// <summary>
    /// EFI byte code
    /// </summary>
    EBC = 0x0ebc,
    /// <summary>
    /// RISC-V 32-bit address space
    /// </summary>
    RISCV32 = 0x5032,
    /// <summary>
    /// RISC-V 64-bit address space
    /// </summary>
    RISCV64 = 0x5064,
    /// <summary>
    /// RISC-V 128-bit address space
    /// </summary>
    RISCV128 = 0x5128,
    /// <summary>
    /// x64
    /// </summary>
    AMD64 = 0x8664,
    /// <summary>
    /// ARM64 little endian
    /// </summary>
    ARM64 = 0xaa64,
    /// <summary>
    /// LoongArch 32-bit processor family
    /// </summary>
    LoongArch32 = 0x6232,
    /// <summary>
    /// LoongArch 64-bit processor family
    /// </summary>
    LoongArch64 = 0x6264,
    /// <summary>
    /// Mitsubishi M32R little endian
    /// </summary>
    M32R = 0x9041
}
    public enum MagicType : ushort
    {
        IMAGE_NT_OPTIONAL_HDR32_MAGIC = 0x10b,
        IMAGE_NT_OPTIONAL_HDR64_MAGIC = 0x20b
    }
    public enum SubSystemType : ushort
    {
        IMAGE_SUBSYSTEM_UNKNOWN = 0,
        IMAGE_SUBSYSTEM_NATIVE = 1,
        IMAGE_SUBSYSTEM_WINDOWS_GUI = 2,
        IMAGE_SUBSYSTEM_WINDOWS_CUI = 3,
        IMAGE_SUBSYSTEM_POSIX_CUI = 7,
        IMAGE_SUBSYSTEM_WINDOWS_CE_GUI = 9,
        IMAGE_SUBSYSTEM_EFI_APPLICATION = 10,
        IMAGE_SUBSYSTEM_EFI_BOOT_SERVICE_DRIVER = 11,
        IMAGE_SUBSYSTEM_EFI_RUNTIME_DRIVER = 12,
        IMAGE_SUBSYSTEM_EFI_ROM = 13,
        IMAGE_SUBSYSTEM_XBOX = 14

    }
    public enum DllCharacteristicsType : ushort
    {
        RES_0 = 0x0001,
        RES_1 = 0x0002,
        RES_2 = 0x0004,
        RES_3 = 0x0008,
        IMAGE_DLL_CHARACTERISTICS_DYNAMIC_BASE = 0x0040,
        IMAGE_DLL_CHARACTERISTICS_FORCE_INTEGRITY = 0x0080,
        IMAGE_DLL_CHARACTERISTICS_NX_COMPAT = 0x0100,
        IMAGE_DLLCHARACTERISTICS_NO_ISOLATION = 0x0200,
        IMAGE_DLLCHARACTERISTICS_NO_SEH = 0x0400,
        IMAGE_DLLCHARACTERISTICS_NO_BIND = 0x0800,
        RES_4 = 0x1000,
        IMAGE_DLLCHARACTERISTICS_WDM_DRIVER = 0x2000,
        IMAGE_DLLCHARACTERISTICS_TERMINAL_SERVER_AWARE = 0x8000
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack:=1)> _
  Public Structure IMAGE_OPTIONAL_HEADER64
    Public Magic As UInt16
    Public MajorLinkerVersion As [Byte]
    Public MinorLinkerVersion As [Byte]
    Public SizeOfCode As UInt32
    Public SizeOfInitializedData As UInt32
    Public SizeOfUninitializedData As UInt32
    Public AddressOfEntryPoint As UInt32
    Public BaseOfCode As UInt32
    Public ImageBase As UInt64
    Public SectionAlignment As UInt32
    Public FileAlignment As UInt32
    Public MajorOperatingSystemVersion As UInt16
    Public MinorOperatingSystemVersion As UInt16
    Public MajorImageVersion As UInt16
    Public MinorImageVersion As UInt16
    Public MajorSubsystemVersion As UInt16
    Public MinorSubsystemVersion As UInt16
    Public Win32VersionValue As UInt32
    Public SizeOfImage As UInt32
    Public SizeOfHeaders As UInt32
    Public CheckSum As UInt32
    Public Subsystem As UInt16
    Public DllCharacteristics As UInt16
    Public SizeOfStackReserve As UInt64
    Public SizeOfStackCommit As UInt64
    Public SizeOfHeapReserve As UInt64
    Public SizeOfHeapCommit As UInt64
    Public LoaderFlags As UInt32
    Public NumberOfRvaAndSizes As UInt32
  End Structure
```
