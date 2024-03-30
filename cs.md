#NtCreateFile

## C# Signature:
```cs
[DllImport("ntdll.dll", ExactSpelling = true, SetLastError = true)]
public static extern int NtCreateFile(out SafeFileHandle handle, FileAccess access, OBJECT_ATTRIBUTES* objectAttributes, IO_STATUS_BLOCK* ioStatus, ref long allocSize, uint fileAttributes, FileShare share, uint createDisposition, uint createOptions, IntPtr eaBuffer, uint eaLength);
```

## C# Signature:
```cs
[DllImport("ntdll.dll", ExactSpelling = true, SetLastError = true)]
    public static extern int NtCreateFile(
        out  Microsoft.Win32.SafeHandles.SafeFileHandle handle,
        System.IO.FileAccess access,
        ref OBJECT_ATTRIBUTES objectAttributes,
        ref IO_STATUS_BLOCK ioStatus,
        ref long allocSize,
        uint fileAttributes,
        System.IO.FileShare share,
        uint createDisposition,
        uint createOptions,
        IntPtr eaBuffer,
        uint eaLength);
```

## VB Signature:
```cs
Declare Function NtCreateFile Lib "ntdll.dll" (TODO) As TODO
```

## Sample Code:
```cs
[StructLayout(LayoutKind.Sequential, Pack = 0)]
public struct IO_STATUS_BLOCK
{
   public uint status;
   public IntPtr information;
}

[StructLayout(LayoutKind.Sequential,Pack=0)]
public struct OBJECT_ATTRIBUTES
{
   public Int32 Length;
   public IntPtr RootDirectory;
   public IntPtr ObjectName;
   public uint Attributes;
   public IntPtr SecurityDescriptor;
   public IntPtr SecurityQualityOfService;

}

[StructLayout(LayoutKind.Sequential, Pack=0)]
public struct UNICODE_STRING 
{
    public ushort Length;
    public ushort MaximumLength;
    public IntPtr Buffer;

}
```

## Sample Code:
```cs
GetPathFromFileReference(UInt64 frn)
{
UInt32 FILE_OPEN = 0x1;
UInt32 FILE_OPEN_BY_FILE_ID = 0x2000;
UInt32 FILE_OPEN_FOR_BACKUP_INTENT = 0x4000;
UInt32 OBJ_CASE_INSENSITIVE = 0x40;
IntPtr _RootHandle; //This will need to be initialized with the root handle, can use CreateFile from kernel32.dll
```

## Sample Code:
```cs
long allocSize = 0;
UNICODE_STRING unicodeString;
OBJECT_ATTRIBUTES objAttributes = new OBJECT_ATTRIBUTES();
IO_STATUS_BLOCK ioStatusBlock = new IO_STATUS_BLOCK();
Microsoft.Win32.SafeHandles.SafeFileHandle hFile;

IntPtr buffer = Marshal.AllocHGlobal(4096);
IntPtr refPtr = Marshal.AllocHGlobal(8);
IntPtr objAttIntPtr = Marshal.AllocHGlobal(Marshal.SizeOf(objAttributes));

//frn = file reference number which is a UInt64
Marshal.WriteInt64(refPtr, (long)frn);

unicodeString.Length = 8;
unicodeString.MaximumLength = 8;
unicodeString.Buffer = refPtr;

objAttributes.Length = System.Convert.ToInt32(Marshal.SizeOf(objAttributes));
objAttributes.ObjectName = objAttIntPtr;
objAttributes.RootDirectory = _RootHandle;
objAttributes.Attributes = OBJ_CASE_INSENSITIVE;
objAttributes.SecurityDescriptor = IntPtr.Zero;
objAttributes.SecurityQualityOfService = IntPtr.Zero;
```

## Sample Code:
```cs
int fOk = Win32Api.NtCreateFile(
                out hFile,
                FileAccess.Read,
                ref objAttributes,
                ref ioStatusBlock,
                ref allocSize,
                System.Convert.ToUInt32(0),
                System.IO.FileShare.Read ,
                FILE_OPEN,
                FILE_OPEN_BY_FILE_ID | FILE_OPEN_FOR_BACKUP_INTENT,
                IntPtr.Zero, System.Convert.ToUInt32(0));
```

## Sample Code:
```cs
//Use NtQueryInformationFile to get information on the file such as path

}
```
