
## C# Definition:
```cs
public enum PARTITION_TYPE : byte
{
    PARTITION_ENTRY_UNUSED = 0x00, // Entry unused
    PARTITION_FAT_12 = 0x01, // 12-bit FAT entries
    PARTITION_XENIX_1 = 0x02, // Xenix
    PARTITION_XENIX_2 = 0x03, // Xenix
    PARTITION_FAT_16 = 0x04, // 16-bit FAT entries
    PARTITION_EXTENDED = 0x05, // Extended partition entry
    PARTITION_HUGE = 0x06, // Huge partition MS-DOS V4
    PARTITION_IFS = 0x07, // IFS Partition
    PARTITION_OS2BOOTMGR = 0x0A, // OS/2 Boot Manager/OPUS/Coherent swap
    PARTITION_FAT32 = 0x0B, // FAT32
    PARTITION_FAT32_XINT13 = 0x0C, // FAT32 using extended int13 services
    PARTITION_XINT13 = 0x0E, // Win95 partition using extended int13 services
    PARTITION_XINT13_EXTENDED = 0x0F, // Same as type 5 but uses extended int13 services
    PARTITION_PREP = 0x41, // PowerPC Reference Platform (PReP) Boot Partition
    PARTITION_LDM = 0x42, // Logical Disk Manager partition
    PARTITION_UNIX = 0x63, // Unix
    VALID_NTFT = 0xC0, // NTFT uses high order bits
    PARTITION_NTFT = 0x80,  // NTFT partition
    PARTITION_LINUX_SWAP = 0x82, //An ext2/ext3/ext4 swap partition
    PARTITION_LINUX_NATIVE = 0x83 //An ext2/ext3/ext4 native partition
}
```

## VB Definition:
```cs
Public Enum PARTITION_TYPE As Byte
    PARTITION_ENTRY_UNUSED = &H0 ' Entry unused
    PARTITION_FAT_12 = &H1 ' 12-bit FAT entries
    PARTITION_XENIX_1 = &H2 ' Xenix
    PARTITION_XENIX_2 = &H3 ' Xenix
    PARTITION_FAT_16 = &H4 ' 16-bit FAT entries
    PARTITION_EXTENDED = &H5 ' Extended partition entry
    PARTITION_HUGE = &H6 ' Huge partition MS-DOS V4
    PARTITION_IFS = &H7 ' IFS Partition
    PARTITION_OS2BOOTMGR = &Ha ' OS/2 Boot Manager/OPUS/Coherent swap
    PARTITION_FAT32 = &Hb ' FAT32
    PARTITION_FAT32_XINT13 = &Hc ' FAT32 using extended int13 services
    PARTITION_XINT13 = &He ' Win95 partition using extended int13 services
    PARTITION_XINT13_EXTENDED = &Hf ' Same as type 5 but uses extended int13 services
    PARTITION_PREP = &H41 ' PowerPC Reference Platform (PReP) Boot Partition
    PARTITION_LDM = &H42 ' Logical Disk Manager partition
    PARTITION_UNIX = &H63 ' Unix
    VALID_NTFT = &Hc0 ' NTFT uses high order bits
    PARTITION_NTFT = &H80 ' NTFT partition
    PARTITION_LINUX_SWAP = &H82 'An ext2/ext3/ext4 swap partition
    PARTITION_LINUX_NATIVE = &H83 'An ext2/ext3/ext4 native partition
End Enum
```
