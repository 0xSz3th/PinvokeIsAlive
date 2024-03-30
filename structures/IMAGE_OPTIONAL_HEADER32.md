
## C# Definition:
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

    [StructLayout(LayoutKind.Explicit)]
    public struct IMAGE_OPTIONAL_HEADER32
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

        // PE32 contains this additional field
        [FieldOffset(24)]
        public uint BaseOfData;

        [FieldOffset(28)]
        public uint ImageBase;

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
        public uint SizeOfStackReserve;

        [FieldOffset(76)]
        public uint SizeOfStackCommit;

        [FieldOffset(80)]
        public uint SizeOfHeapReserve;

        [FieldOffset(84)]
        public uint SizeOfHeapCommit;

        [FieldOffset(88)]
        public uint LoaderFlags;

        [FieldOffset(92)]
        public uint NumberOfRvaAndSizes;

        [FieldOffset(96)]
        public IMAGE_DATA_DIRECTORY ExportTable;

        [FieldOffset(104)]
        public IMAGE_DATA_DIRECTORY ImportTable;

        [FieldOffset(112)]
        public IMAGE_DATA_DIRECTORY ResourceTable;

        [FieldOffset(120)]
        public IMAGE_DATA_DIRECTORY ExceptionTable;

        [FieldOffset(128)]
        public IMAGE_DATA_DIRECTORY CertificateTable;

        [FieldOffset(136)]
        public IMAGE_DATA_DIRECTORY BaseRelocationTable;

        [FieldOffset(144)]
        public IMAGE_DATA_DIRECTORY Debug;

        [FieldOffset(152)]
        public IMAGE_DATA_DIRECTORY Architecture;

        [FieldOffset(160)]
        public IMAGE_DATA_DIRECTORY GlobalPtr;

        [FieldOffset(168)]
        public IMAGE_DATA_DIRECTORY TLSTable;

        [FieldOffset(176)]
        public IMAGE_DATA_DIRECTORY LoadConfigTable;

        [FieldOffset(184)]
        public IMAGE_DATA_DIRECTORY BoundImport;

        [FieldOffset(192)]
        public IMAGE_DATA_DIRECTORY IAT;

        [FieldOffset(200)]
        public IMAGE_DATA_DIRECTORY DelayImportDescriptor;

        [FieldOffset(208)]
        public IMAGE_DATA_DIRECTORY CLRRuntimeHeader;

        [FieldOffset(216)]
        public IMAGE_DATA_DIRECTORY Reserved;
    }
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

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack:=1)> _
    Public Structure IMAGE_OPTIONAL_HEADER32
    ''' <summary> 
    ''' A signature WORD, identifying what type of header this is. The two most  
    ''' common values are IMAGE_NT_OPTIONAL_HDR32_MAGIC 0x10b and  
    ''' IMAGE_NT_OPTIONAL_HDR64_MAGIC 0x20b. 
    ''' </summary> 
    Public Magic As UInt16

    ''' <summary> 
    ''' The major version of the linker used to build this executable. For PE files 
    ''' from the Microsoft linker, this version number corresponds to the Visual  
    ''' Studio version number (for example, version 6 for Visual Studio 6.0). 
    ''' </summary> 
    Public MajorLinkerVersion As Byte

    ''' <summary> 
    ''' The minor version of the linker used to build this executable. 
    ''' </summary> 
    Public MinorLinkerVersion As Byte

    ''' <summary> 
    ''' The combined total size of all sections with the IMAGE_SCN_CNT_CODE attribute. 
    ''' </summary> 
    Public SizeOfCode As UInt32

    ''' <summary> 
    ''' The combined size of all initialized data sections. 
    ''' </summary> 
    Public SizeOfInitializedData As UInt32

    ''' <summary> 
    ''' The size of all sections with the uninitialized data attributes. This field  
    ''' will often be 0, since the linker can append uninitialized data to the end 
    ''' of regular data sections. 
    ''' </summary> 
    Public SizeOfUninitializedData As UInt32

    ''' <summary> 
    ''' The RVA of the first code byte in the file that will be executed. For DLLs,  
    ''' this entrypoint is called during process initialization and shutdown and  
    ''' during thread creations/destructions. In most executables, this address  
    ''' doesn't directly point to main, WinMain, or DllMain. Rather, it points to  
    ''' runtime library code that calls the aforementioned functions. This field can  
    ''' be set to 0 in DLLs, and none of the previous notifications will be received. 
    ''' The linker /NOENTRY switch sets this field to 0. 
    ''' </summary> 
    Public AddressOfEntryPoint As UInt32

    ''' <summary> 
    ''' The RVA of the first byte of code when loaded in memory. 
    ''' </summary> 
    Public BaseOfCode As UInt32
```

## VB Definition:
```cs
''' <summary> 
    ''' Theoretically, the RVA of the first byte of data when loaded into memory.  
    ''' However, the values for this field are inconsistent with different versions  
    ''' of the Microsoft linker. This field is not present in 64-bit executables. 
    ''' </summary> 
    Public BaseOfData As UInt32

    ''' <summary> 
    ''' The preferred load address of this file in memory. The loader attempts to  
    ''' load the PE file at this address if possible (that is, if nothing else  
    ''' currently occupies that memory, it's aligned properly and at a legal address,  
    ''' and so on). If the executable loads at this address, the loader can skip the  
    ''' step of applying base relocations (described in Part 2 of this article).  
    ''' For EXEs, the default ImageBase is 0x400000. For DLLs, it's 0x10000000.  
    ''' The ImageBase can be set at link time with the /BASE switch, or later with the  
    ''' REBASE utility. 
    ''' </summary> 
    Public ImageBase As UInt32

    ''' <summary> 
    ''' The alignment of sections when loaded into memory. The alignment must be  
    ''' greater or equal to the file alignment field (mentioned next). The default  
    ''' alignment is the page size of the target CPU. For user mode executables to  
    ''' run under Windows 9x or Windows Me, the minimum alignment size is a page (4KB). 
    ''' This field can be set with the linker /ALIGN switch. 
    ''' </summary> 
    Public SectionAlignment As UInt32

    ''' <summary> 
    ''' The alignment of sections within the PE file. For x86 executables, this value  
    ''' is usually either 0x200 or 0x1000. The default has changed with different  
    ''' versions of the Microsoft linker. This value must be a power of 2, and if the  
    ''' SectionAlignment is less than the CPU's page size, this field must match the  
    ''' SectionAlignment. The linker switch /OPT:WIN98 sets the file alignment on x86  
    ''' executables to 0x1000, while /OPT:NOWIN98 sets the alignment to 0x200. 
    ''' </summary> 
    Public FileAlignment As UInt32

    ''' <summary> 
    ''' The major version number of the required operating system. With the advent  
    ''' of so many versions of Windows, this field has effectively become irrelevant. 
    ''' </summary> 
    Public MajorOperatingSystemVersion As UInt16

    ''' <summary> 
    ''' The minor version number of the required OS. 
    ''' </summary> 
    Public MinorOperatingSystemVersion As UInt16

    ''' <summary> 
    ''' The major version number of this file. Unused by the system and can be 0.  
    ''' It can be set with the linker /VERSION switch. 
    ''' </summary> 
    Public MajorImageVersion As UInt16

    ''' <summary> 
    ''' The minor version number of this file. 
    ''' </summary> 
    Public MinorImageVersion As UInt16

    ''' <summary> 
    ''' The major version of the operating subsystem needed for this executable.  
    ''' At one time, it was used to indicate that the newer Windows 95 or Windows NT 4.0  
    ''' user interface was required, as opposed to older versions of the Windows NT  
    ''' interface. Today, because of the proliferation of the various versions of  
    ''' Windows, this field is effectively unused by the system and is typically set  
    ''' to the value 4. Set with the linker /SUBSYSTEM switch. 
    ''' </summary> 
    Public MajorSubsystemVersion As UInt16

    ''' <summary> 
    ''' The minor version of the operating subsystem needed for this executable. 
    ''' </summary> 
    Public MinorSubsystemVersion As UInt16

    ''' <summary> 
    ''' Another field that never took off. Typically set to 0. 
    ''' </summary> 
    Public Win32VersionValue As UInt32

    ''' <summary> 
    ''' SizeOfImage contains the RVA that would be assigned to the section following  
    ''' the last section if it existed. This is effectively the amount of memory that  
    ''' the system needs to reserve when loading this file into memory. This field 
    ''' must be a multiple of the section alignment. 
    ''' </summary> 
    Public SizeOfImage As UInt32

    ''' <summary> 
    ''' The combined size of the MS-DOS header, PE headers, and section table. All of  
    ''' these items will occur before any code or data sections in the PE file. The  
    ''' value of this field is rounded up to a multiple of the file alignment.  
    ''' </summary> 
    Public SizeOfHeaders As UInt32

    ''' <summary> 
    ''' The checksum of the image. The CheckSumMappedFile API in IMAGEHLP.DLL can  
    ''' calculate this value. Checksums are required for kernel-mode drivers and some  
    ''' system DLLs. Otherwise, this field can be 0. The checksum is placed in the  
    ''' file when the /RELEASE linker switch is used. 
    ''' </summary> 
    Public CheckSum As UInt32
```

## VB Definition:
```cs
''' <summary> 
    ''' An enum value indicating what subsystem (user interface type) the executable  
    ''' expects. This field is only important for EXEs. Important values include: 
    ''' IMAGE_SUBSYSTEM_NATIVE       // Image doesn't require a subsystem 
    ''' IMAGE_SUBSYSTEM_WINDOWS_GUI  // Use the Windows GUI 
    ''' IMAGE_SUBSYSTEM_WINDOWS_CUI  // Run as a console mode application 
    '''                  // When run, the OS creates a console 
    '''                  // window for it, and provides stdin, 
    '''                  // stdout, and stderr file handles 
    ''' 
    ''' </summary> 
    Public Subsystem As UInt16

    ''' <summary> 
    ''' Flags indicating characteristics of this DLL. These correspond to the  
    ''' IMAGE_DLLCHARACTERISTICS_xxx fields #defines. Current values are: 
    ''' IMAGE_DLLCHARACTERISTICS_NO_BIND    // Do not bind this image 
    ''' IMAGE_DLLCHARACTERISTICS_WDM_DRIVER    // Driver uses WDM model 
    ''' IMAGE_DLLCHARACTERISTICS_TERMINAL_SERVER_AWARE // When the terminal server loads 
    '''                        // an application that is not 
    '''                        //  Terminal- Services-aware, it 
    '''                        // also loads a DLL that contains 
    '''                        // compatibility code 
    ''' </summary> 
    Public DllCharacteristics As UInt16

    ''' <summary> 
    ''' In EXE files, the maximum size the initial thread in the process can grow to.  
    ''' This is 1MB by default. Not all this memory is committed initially. 
    ''' </summary> 
    Public SizeOfStackReserve As UInt32

    ''' <summary> 
    ''' In EXE files, the amount of memory initially committed to the stack.  
    ''' By default, this field is 4KB. 
    ''' </summary> 
    Public SizeOfStackCommit As UInt32

    ''' <summary> 
    ''' In EXE files, the initial reserved size of the default process heap.  
    ''' This is 1MB by default. In current versions of Windows, however,  
    ''' the heap can grow beyond this size without intervention by the user. 
    ''' </summary> 
    Public SizeOfHeapReserve As UInt32

    ''' <summary> 
    ''' In EXE files, the size of memory committed to the heap.  
    ''' By default, this is 4KB. 
    ''' </summary> 
    Public SizeOfHeapCommit As UInt32

    ''' <summary> 
    ''' This is obsolete. 
    ''' </summary> 
    Public LoaderFlags As UInt32
```

## VB Definition:
```cs
''' <summary> 
    '''  At the end of the IMAGE_NT_HEADERS structure is an array of  
    '''  IMAGE_DATA_DIRECTORY structures. This field contains the number of entries in 
    '''  the array. This field has been 16 since the earliest releases of Windows NT. 
    ''' </summary> 
    Public NumberOfRvaAndSizes As UInt32

    ''' <summary> 
    '''  A pointer to the first IMAGE_DATA_DIRECTORY structure in the data directory.
    '''  The number of directories is not fixed. Check the NumberOfRvaAndSizes member before looking for a specific directory.
    ''' </summary> 
    Public DataDirectory(15) As IMAGE_DATA_DIRECTORY
  End Structure
```

## VB 6 Definition:
```cs
Public Type IMAGE_OPTIONAL_HEADER32
    '---- Standard fields. ----
    ' A signature WORD, identifying what type of header this is.
    ' The common values are IMAGE_NT_OPTIONAL_HDR32_MAGIC 0x10b and IMAGE_NT_OPTIONAL_HDR64_MAGIC 0x20b.
    Magic As Integer
    ' The major version of the linker used to build this executable.  For PE files from the Microsoft
    ' linker, this corresponds to the Visual Studio version (ex. 6 for Visual Studio 6.0).
    MajorLinkerVersion As Byte
    ' The minor version of the linker used to build this executable.
    MinorLinkerVersion As Byte
    ' The combined total size of all sections with the IMAGE_SCN_CNT_CODE attribute.
    SizeOfCode As Long
    ' The combined size of all initialized data sections.
    SizeOfInitializedData As Long
    ' The size of all sections with the uninitialized data attributes.  This field will often be 0,
    ' since the linker can append uninitialized data to the end of regular data sections.
    SizeOfUninitializedData As Long
    ' A pointer to the entry point function, relative to the image base address (The relative virtual
    ' address (RVA) of the first code byte in the file that will be executed.)  For DLLs, this
    ' entrypoint is called during process initialization and shutdown and during thread creations/
    ' destructions.  In most executables, this address doesn't directly point to main, WinMain,
    ' or DllMain, rather, it points to runtime library code that calls the aforementioned functions.
    ' This field can be set to 0 in DLLs, and none of the previous notifications will be received.
    ' The linker /NOENTRY switch sets this field to 0.
    AddressOfEntryPoint As Long
    ' The relative virtual address of the first byte of code when loaded in memory.
    BaseOfCode As Long
    ' Theoretically, the relative virtual address of the first byte of data when loaded into memory.
    ' However, values for this field are inconsistent with different versions of the Microsoft linker.
    ' This field is not present in 64-bit executables.
    BaseOfData As Long

    '---- NT additional fields. ----
    ' The preferred load address of this file in memory.  The loader attempts to load the PE file at
    ' this address if possible (if nothing else currently occupies that memory, it's aligned properly,
    ' at a legal address, and so on). If the executable loads at this address, the loader can skip the
    ' step of applying base relocations. The default ImageBase is for EXEs 0x400000, for DLLs 0x10000000.
    ' The ImageBase can be set at link time with the /BASE switch, or later with the REBASE utility.
    ImageBase As Long
    ' The alignment of sections when loaded into memory.  The alignment must be greater or equal to the
    ' file alignment field.  The default alignment is the page size of the target CPU.  For user mode
    ' executables to run under Windows 9x or Windows Me, the minimum alignment size is a page (4KB).
    ' This field can be set with the linker /ALIGN switch.
    SectionAlignment As Long
    ' The alignment of sections within the PE file.  For x86 executables, this value is usually either
    ' 0x200 (/OPT:WIN98) or 0x1000 (/OPT:NOWIN98).  The default has changed with different versions of
    ' the Microsoft linker.  This value must be a power of 2, and if the SectionAlignment is less than
    ' the CPU's page size, this field must match the SectionAlignment.
    FileAlignment As Long
    ' The major version number of the required operating system.
    ' With the advent of so many versions of Windows, this field has effectively become irrelevant.
    MajorOperatingSystemVersion As Integer
    ' The minor version number of the required OS.
    MinorOperatingSystemVersion As Integer
    ' The major version number of this file.  Unused by the system and can be 0.
    ' It can be set with the linker /VERSION switch.
    MajorImageVersion As Integer
    ' The minor version number of this file.
    MinorImageVersion As Integer
    ' The major version of the operating subsystem needed for this executable.
    ' At one time, it was used to indicate that the newer Windows 95 or Windows NT 4.0 user interface was
    ' required, as opposed to older versions of the Windows NT interface.  Today, because of the
    ' proliferation of the various versions of Windows, this field is effectively unused by the system
    ' and is typically set to the value 4.  Set with the linker /SUBSYSTEM switch.
    MajorSubsystemVersion As Integer
    ' The minor version of the operating subsystem needed for this executable.
    MinorSubsystemVersion As Integer
    ' Another field that never took off.  Typically set to 0.
    Win32VersionValue As Long
    ' SizeOfImage contains the RVA that would be assigned to the section following the last section if it
    ' existed.  This is effectively the amount of memory that the system needs to reserve when loading
    ' this file into memory.  This field must be a multiple of the section alignment.
    SizeOfImage As Long
    ' The combined size of the MS-DOS header, PE headers, and section table.  All of these items will
    ' occur before any code or data sections in the PE file.  The value of this field is rounded up to
    ' a multiple of the file alignment.
    SizeOfHeaders As Long
    ' The checksum of the image.  The CheckSumMappedFile API in IMAGEHLP.DLL can calculate this value.
    ' Checksums are required for kernel-mode drivers and some system DLLs.  Otherwise, this field
    ' can be 0.  The checksum is placed in the file when the /RELEASE linker switch is used.
    CheckSum As Long
    ' An enum value indicating what subsystem (user interface type) the executable expects.
    ' This field is only important for EXEs. Important values include:
    ' IMAGE_SUBSYSTEM_NATIVE (Image doesn't require a subsystem)
    ' IMAGE_SUBSYSTEM_WINDOWS_GUI (Use the Windows GUI)
    ' IMAGE_SUBSYSTEM_WINDOWS_CUI (Run as a console mode application.  When run, the OS creates a 
    '   console window for it, and provides stdin, stdout, and stderr file handles)
    Subsystem As Integer
    ' Flags indicating characteristics of this DLL represented by IMAGE_DLLCHARACTERISTICS_xxx #defines.
    ' Some values are: IMAGE_DLLCHARACTERISTICS_NO_BIND (Do not bind this image)
    ' IMAGE_DLLCHARACTERISTICS_WDM_DRIVER (Driver uses WDM model)
    ' IMAGE_DLLCHARACTERISTICS_TERMINAL_SERVER_AWARE (When the terminal server loads an application
    '   that is not Terminal- Services-aware, it also loads a DLL that contains compatibility code)
    DllCharacteristics As Integer
    ' In EXE files, max size the initial thread in the process can grow to (1MB by default).
    ' Not all memory is committed initially.
    SizeOfStackReserve As Long
    ' In EXE files, the amount of memory initially committed to the stack.  Default is 4KB.
    SizeOfStackCommit As Long
    ' In EXE files, the initial reserved size of the default process heap.  Default is 1MB.
    ' In current versions of Windows, however, the heap can grow beyond this without user intervention.
    SizeOfHeapReserve As Long
    ' In EXE files, the size of memory committed to the heap.  By default, this is 4KB.
    SizeOfHeapCommit As Long
    ' This is obsolete.
    LoaderFlags As Long
    ' At the end of the IMAGE_NT_HEADERS structure is an array of IMAGE_DATA_DIRECTORY structures.
    ' This field contains the number of array entries. (has been 16 since earliest releases of NT)
    NumberOfRvaAndSizes As Long
    ' A pointer to the first IMAGE_DATA_DIRECTORY structure in the data directory.  The number of
    ' directories is not fixed.  Check NumberOfRvaAndSizes before looking for a specific directory.
    DataDirectory(0 To 15) As IMAGE_DATA_DIRECTORY
  End Type

--------------------------------------------------------------------------------------------------------

  Public Type Int64 'LowBytes must be first in LittleEndian systems (For IMAGE_OPTIONAL_HEADER64)
    LowBytes  As Long
    HighBytes As Long
  End Type

  Public Type IMAGE_OPTIONAL_HEADER64
    '---- Standard fields. ----
    ' A signature WORD, identifying what type of header this is.
    ' The common values are IMAGE_NT_OPTIONAL_HDR32_MAGIC 0x10b and IMAGE_NT_OPTIONAL_HDR64_MAGIC 0x20b.
    Magic As Integer
    ' The major version of the linker used to build this executable.  For PE files from the Microsoft
    ' linker, this corresponds to the Visual Studio version (ex. 6 for Visual Studio 6.0).
    MajorLinkerVersion As Byte
    ' The minor version of the linker used to build this executable.
    MinorLinkerVersion As Byte
    ' The combined total size of all sections with the IMAGE_SCN_CNT_CODE attribute.
    SizeOfCode As Long
    ' The combined size of all initialized data sections.
    SizeOfInitializedData As Long
    ' The size of all sections with the uninitialized data attributes.  This field will often be 0,
    ' since the linker can append uninitialized data to the end of regular data sections.
    SizeOfUninitializedData As Long
    ' A pointer to the entry point function, relative to the image base address (The relative virtual
    ' address (RVA) of the first code byte in the file that will be executed.)  For DLLs, this
    ' entrypoint is called during process initialization and shutdown and during thread creations/
    ' destructions.  In most executables, this address doesn't directly point to main, WinMain,
    ' or DllMain, rather, it points to runtime library code that calls the aforementioned functions.
    ' This field can be set to 0 in DLLs, and none of the previous notifications will be received.
    ' The linker /NOENTRY switch sets this field to 0.
    AddressOfEntryPoint As Long
    ' The relative virtual address of the first byte of code when loaded in memory.
    BaseOfCode As Long

    '---- NT additional fields. ----
    ' The preferred load address of this file in memory.  The loader attempts to load the PE file at
    ' this address if possible (if nothing else currently occupies that memory, it's aligned properly,
    ' at a legal address, and so on). If the executable loads at this address, the loader can skip the
    ' step of applying base relocations.
    ' The ImageBase can be set at link time with the /BASE switch, or later with the REBASE utility.
    ImageBase As Int64
    ' The alignment of sections when loaded into memory.  The alignment must be greater or equal to the
    ' file alignment field.  The default alignment is the page size of the target CPU.  For user mode
    ' executables to run under Windows 9x or Windows Me, the minimum alignment size is a page (4KB).
    ' This field can be set with the linker /ALIGN switch.
    SectionAlignment As Long
    ' The alignment of sections within the PE file.  For x86 executables, this value is usually either
    ' 0x200 (/OPT:WIN98) or 0x1000 (/OPT:NOWIN98).  The default has changed with different versions of
    ' the Microsoft linker.  This value must be a power of 2, and if the SectionAlignment is less than
    ' the CPU's page size, this field must match the SectionAlignment.
    FileAlignment As Long
    ' The major version number of the required operating system.
    ' With the advent of so many versions of Windows, this field has effectively become irrelevant.
    MajorOperatingSystemVersion As Integer
    ' The minor version number of the required OS.
    MinorOperatingSystemVersion As Integer
    ' The major version number of this file.  Unused by the system and can be 0.
    ' It can be set with the linker /VERSION switch.
    MajorImageVersion As Integer
    ' The minor version number of this file.
    MinorImageVersion As Integer
    ' The major version of the operating subsystem needed for this executable.
    ' At one time, it was used to indicate that the newer Windows 95 or Windows NT 4.0 user interface was
    ' required, as opposed to older versions of the Windows NT interface.  Today, because of the
    ' proliferation of the various versions of Windows, this field is effectively unused by the system
    ' and is typically set to the value 4.  Set with the linker /SUBSYSTEM switch.
    MajorSubsystemVersion As Integer
    ' The minor version of the operating subsystem needed for this executable.
    MinorSubsystemVersion As Integer
    ' Another field that never took off.  Typically set to 0.
    Win32VersionValue As Long
    ' SizeOfImage contains the RVA that would be assigned to the section following the last section if it
    ' existed.  This is effectively the amount of memory that the system needs to reserve when loading
    ' this file into memory.  This field must be a multiple of the section alignment.
    SizeOfImage As Long
    ' The combined size of the MS-DOS header, PE headers, and section table.  All of these items will
    ' occur before any code or data sections in the PE file.  The value of this field is rounded up to
    ' a multiple of the file alignment.
    SizeOfHeaders As Long
    ' The checksum of the image.  The CheckSumMappedFile API in IMAGEHLP.DLL can calculate this value.
    ' Checksums are required for kernel-mode drivers and some system DLLs.  Otherwise, this field
    ' can be 0.  The checksum is placed in the file when the /RELEASE linker switch is used.
    CheckSum As Long
    ' An enum value indicating what subsystem (user interface type) the executable expects.
    ' This field is only important for EXEs. Important values include:
    ' IMAGE_SUBSYSTEM_NATIVE (Image doesn't require a subsystem)
    ' IMAGE_SUBSYSTEM_WINDOWS_GUI (Use the Windows GUI)
    ' IMAGE_SUBSYSTEM_WINDOWS_CUI (Run as a console mode application.  When run, the OS creates a 
    '   console window for it, and provides stdin, stdout, and stderr file handles)
    Subsystem As Integer
    ' Flags indicating characteristics of this DLL represented by IMAGE_DLLCHARACTERISTICS_xxx #defines.
    ' Some values are: IMAGE_DLLCHARACTERISTICS_NO_BIND (Do not bind this image)
    ' IMAGE_DLLCHARACTERISTICS_WDM_DRIVER (Driver uses WDM model)
    ' IMAGE_DLLCHARACTERISTICS_TERMINAL_SERVER_AWARE (When the terminal server loads an application
    '   that is not Terminal- Services-aware, it also loads a DLL that contains compatibility code)
    DllCharacteristics As Integer
    ' In EXE files, max size the initial thread in the process can grow to (1MB by default).
    ' Not all memory is committed initially.
    SizeOfStackReserve As Int64
    ' In EXE files, the amount of memory initially committed to the stack.  Default is 4KB.
    SizeOfStackCommit As Int64
    ' In EXE files, the initial reserved size of the default process heap.  Default is 1MB.
    ' In current versions of Windows, however, the heap can grow beyond this without user intervention.
    SizeOfHeapReserve As Int64
    ' In EXE files, the size of memory committed to the heap.  By default, this is 4KB.
    SizeOfHeapCommit As Int64
    ' This is obsolete.
    LoaderFlags As Long
    ' At the end of the IMAGE_NT_HEADERS structure is an array of IMAGE_DATA_DIRECTORY structures.
    ' This field contains the number of array entries. (has been 16 since earliest releases of NT)
    NumberOfRvaAndSizes As Long
    ' A pointer to the first IMAGE_DATA_DIRECTORY structure in the data directory.  The number of
    ' directories is not fixed.  Check NumberOfRvaAndSizes before looking for a specific directory.
    DataDirectory(0 To 15) As IMAGE_DATA_DIRECTORY
  End Type
```
