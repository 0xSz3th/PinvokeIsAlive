
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct IMAGE_FILE_HEADER
{
    public UInt16 Machine;
    public UInt16 NumberOfSections;
    public UInt32 TimeDateStamp;
    public UInt32 PointerToSymbolTable;
    public UInt32 NumberOfSymbols;
    public UInt16 SizeOfOptionalHeader;
    public UInt16 Characteristics;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack:=1)> _
    Public Structure IMAGE_FILE_HEADER
    ''' <summary> 
    ''' The target CPU for this executable.  
    ''' Common values are: IMAGE_FILE_MACHINE_I386    0x014c // Intel 386 
    '''            IMAGE_FILE_MACHINE_IA64    0x0200 // Intel 64 
    '''            IMAGE_FILE_MACHINE_AMD64   0x8664 // AMD 64  
    ''' </summary> 
    Public Machine As UInt16

    ''' <summary> 
    ''' Indicates how many sections are in the section table. The section table 
    ''' immediately follows the IMAGE_NT_HEADERS. 
    ''' </summary> 
    Public NumberOfSections As UInt16

    ''' <summary> 
    ''' Indicates the time when the file was created. This value is the number  
    ''' of seconds since January 1, 1970, Greenwich Mean Time (GMT). This value  
    ''' is a more accurate indicator of when the file was created than is the  
    ''' file system date/time. 
    ''' </summary> 
    Public TimeDateStamp As UInt32

    ''' <summary> 
    ''' The file offset of the COFF symbol table, described in section 5.4 of the  
    ''' Microsoft specification. COFF symbol tables are relatively rare in PE files, 
    ''' as newer debug formats have taken over. Prior to Visual Studio .NET,  
    ''' a COFF symbol table could be created by specifying the linker switch 
    ''' /DEBUGTYPE:COFF. COFF symbol tables are almost always found in OBJ files.  
    ''' Set to 0 if no symbol table is present. 
    ''' </summary> 
    Public PointerToSymbolTable As UInt32

    ''' <summary> 
    ''' Number of symbols in the COFF symbol table, if present. COFF symbols are a  
    ''' fixed size structure, and this field is needed to find the end of the COFF  
    ''' symbols. Immediately following the COFF symbols is a string table used to  
    ''' hold longer symbol names. 
    ''' </summary> 
    Public NumberOfSymbols As UInt32

    ''' <summary> 
    ''' The size of the optional data that follows the IMAGE_FILE_HEADER. In PE files, 
    ''' this data is the IMAGE_OPTIONAL_HEADER. This size is different depending on  
    ''' whether it's a 32 or 64-bit file. For 32-bit PE files, this field is usually  
    ''' 224. For 64-bit PE32+ files, it's usually 240. However, these sizes are just  
    ''' minimum values, and larger values could appear. 
    ''' </summary> 
    Public SizeOfOptionalHeader As UInt16

    ''' <summary> 
    ''' A set of bit flags indicating attributes of the file.  
    ''' </summary> 
    Public Characteristics As UInt16

  End Structure

  <Flags()> Public Enum IFHMachine As UInt16
    x86 = &H14C
    Alpha = &H184
    ARM = &H1C0
    MIPS16R3000 = &H162
    MIPS16R4000 = &H166
    MIPS16R10000 = &H168
    PowerPCLE = &H1F0
    PowerPCBE = &H1F2
    Itanium = &H200
    MIPS16 = &H266
    Alpha64 = &H284
    MIPSFPU = &H366
    MIPSFPU16 = &H466
    x64 = &H8664
  End Enum

  <Flags()> Public Enum IFHCharacteristics As UInt16
    RelocationInformationStrippedFromFile = &H1
    Executable = &H2
    LineNumbersStripped = &H4
    SymbolTableStripped = &H8
    AggresiveTrimWorkingSet = &H10
    LargeAddressAware = &H20
    Supports16Bit = &H40
    ReservedBytesWo = &H80
    Supports32Bit = &H100
    DebugInfoStripped = &H200
    RunFromSwapIfInRemovableMedia = &H400
    RunFromSwapIfInNetworkMedia = &H800
    IsSytemFile = &H1000
    IsDLL = &H2000
    IsOnlyForSingleCoreProcessor = &H4000
    BytesOfWordReserved = &H8000
  End Enum
```

## VB 6 Definition:
```cs
Public Type IMAGE_FILE_HEADER
      ' The target CPU for this executable.  Common values are:
      ' IMAGE_FILE_MACHINE_I386 = 0x014c (Intel 386)
      ' IMAGE_FILE_MACHINE_IA64 = 0x0200 (Intel 64)
      ' IMAGE_FILE_MACHINE_AMD64 = 0x8664 (AMD 64)
      Machine As Integer
      ' Number of sections are in the section table which immediately follows the IMAGE_NT_HEADERS.
      NumberOfSections As Integer
      ' Indicates the time when the file was created. This value is the number of seconds since
      ' January 1, 1970, Greenwich Mean Time (GMT).  This value is a more accurate indicator of
      ' when the file was created than is the file system date/time.
      TimeDateStamp As Long
      ' The file offset of the COFF symbol table, described in section 5.4 of the Microsoft
      ' specification.  COFF symbol tables are relatively rare in PE files, as newer debug
      ' formats have taken over.  Prior to Visual Studio .NET, a COFF symbol table could be
      ' created by specifying the linker switch /DEBUGTYPE:COFF.  COFF symbol tables are almost
      ' always found in OBJ files.  Set to 0 if no symbol table is present.
      PointerToSymbolTable As Long
      ' Number of symbols in the COFF symbol table, if present.  COFF symbols are a fixed size 
      'structure, and this field is needed to find the end of the COFF symbols.
      ' Immediately following the COFF symbols is a string table used to hold longer symbol names.
      NumberOfSymbols As Long
      ' The size of the optional data that follows the IMAGE_FILE_HEADER. In PE files, this data
      ' is the IMAGE_OPTIONAL_HEADER.  This size is different depending on whether it's a 32 or
      ' 64-bit file. For 32-bit PE files, this field is usually 224.  For 64-bit PE32+ files,
      ' it's usually 240. However, these are just minimum values, and larger values could appear.
      SizeOfOptionalHeader As Integer
      ' A set of bit flags indicating attributes of the file.  
      Characteristics As Integer
  End Type
```
