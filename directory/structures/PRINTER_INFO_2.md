
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
    public struct PRINTER_INFO_2
    {
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pServerName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pPrinterName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pShareName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pPortName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pDriverName;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pComment;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pLocation;
        public IntPtr pDevMode;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pSepFile;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pPrintProcessor;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pDatatype;
        [MarshalAs(UnmanagedType.LPTStr)]
        public string pParameters;
        public IntPtr pSecurityDescriptor;
        public uint Attributes; // See note below!
        public uint Priority;
        public uint DefaultPriority;
        public uint StartTime;
        public uint UntilTime;
        public uint Status;
        public uint cJobs;
        public uint AveragePPM;
    }
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Private Structure PRINTER_INFO_2

        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pServerName As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pPrinterName As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pShareName As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pPortName As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pDriverName As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pComment As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pLocation As String

        Public pDevMode As IntPtr

        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pSepFile As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pPrintProcessor As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pDatatype As String
        <MarshalAs(UnmanagedType.LPTStr)> _
        Public pParameters As String

        Public pSecurityDescriptor As IntPtr
        Public Attributes As Integer
        Public Priority As Integer
        Public DefaultPriority As Integer
        Public StartTime As Integer
        Public UntilTime As Integer
        Public Status As Integer
        Public cJobs As Integer
        Public AveragePPM As Integer

    End Structure
```

## Notes:
```cs
public uint Attributes;
```

## Notes:
```cs
public PRINTER_ATTRIBUTES Attributes;
```
