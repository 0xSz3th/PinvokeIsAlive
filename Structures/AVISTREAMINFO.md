
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
public struct AVISTREAMINFO 
{
            public Int32    fccType;
            public Int32    fccHandler;
            public Int32    dwFlags;
            public Int32    dwCaps;
            public Int16    wPriority;
            public Int16    wLanguage;
            public Int32    dwScale;
            public Int32    dwRate;
            public Int32    dwStart;
            public Int32    dwLength;
            public Int32    dwInitialFrames;
            public Int32    dwSuggestedBufferSize;
            public Int32    dwQuality;
            public Int32    dwSampleSize;
            public RECT        rcFrame;
            public Int32    dwEditCount;
            public Int32    dwFormatChangeCount;
            [MarshalAs(UnmanagedType.ByValArray, SizeConst=64)]
            public String    szName;
}
```

## VB Definition:
```cs
Structure AVISTREAMINFO 
    Public fccType As Int32
    Public fccHandler As Int32
    Public dwFlags As Int32
    Public dwCaps As Int32
    Public wPriority As Int16
    Public wLanguage As Int16
    Public dwScale As Int32
    Public dwRate As Int32
    Public dwStart As Int32
    Public dwLength As Int32
    Public dwInitialFrames As Int32
    Public dwSuggestedBufferSize As Int32
    Public dwQuality As Int32
    Public dwSampleSize As Int32
    Public rcFrame As RECT
    Public dwEditCount As Int32
    Public dwFormatChangeCount As Int32
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=64)> Public szName As String
    End Structure
```
