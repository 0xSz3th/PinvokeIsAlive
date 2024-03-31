
## C# Definition:
```cs
[ComImport]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("79EAC9E5-BAF9-11CE-8C82-00AA004BA90B")]
```

## C# Definition:
```cs
void Switch(ref _tagPROTOCOLDATA pProtocolData);
    void ReportProgress(uint ulStatusCode, [MarshalAs(UnmanagedType.LPWStr)] string szStatusText);
    void ReportData(BSCF grfBSCF, uint ulProgress, uint ulProgressMax);
    void ReportResult(int hrResult, uint dwError, [MarshalAs(UnmanagedType.LPWStr)] string szResult);
```

## VB Definition:
```cs
<ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("79EAC9E5-BAF9-11CE-8C82-00AA004BA90B")> _
```

## VB Definition:
```cs
Sub Switch(ByRef pProtocolData As _tagPROTOCOLDATA)
    Sub ReportProgress(ByVal ulStatusCode As UInt32, <MarshalAs(UnmanagedType.LPWStr)> ByVal szStatusText As String)
    Sub ReportData(ByVal grfBSCF As BSCF, ByVal ulProgress As UInt32, ByVal ulProgressMax As UInt32)
    Sub ReportResult(ByVal hrResult As Integer, ByVal dwError As UInt32, <MarshalAs(UnmanagedType.LPWStr)> ByVal szResult As String)
```
