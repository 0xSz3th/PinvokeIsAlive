
## C# Definition:
```cs
[ComImport]
    [Guid("E357FCCD-A995-4576-B01F-234630154E96")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    interface IThumbnailProvider {
        void GetThumbnail(
            int cx,
            out IntPtr phbmp,
            out WTS_ALPHATYPE pdwAlpha
            );
    }
```

## User-Defined Types (C#):
```cs
enum WTS_ALPHATYPE {
        WTSAT_UNKNOWN = 0,
        WTSAT_RGB = 1,
        WTSAT_ARGB = 2,
    }
```

## VB Definition:
```cs
<ComImport> _
    <Guid("E357FCCD-A995-4576-B01F-234630154E96")> _
    <InterfaceType(ComInterfaceType.InterfaceIsIUnknown)> _
    Interface IThumbnailProvider
        Sub GetThumbnail(cx As Integer, ByRef phbmp As IntPtr, ByRef pdwAlpha As WTS_ALPHATYPE)
    End Interface
```

## User-Defined Types (VB):
```cs
Enum WTS_ALPHATYPE
        WTSAT_UNKNOWN = 0
        WTSAT_RGB = 1
        WTSAT_ARGB = 2
    End Enum
```
