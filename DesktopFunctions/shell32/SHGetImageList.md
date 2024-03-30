
## C# Signature:
```cs
[DllImport("shell32.dll", EntryPoint = "#727")]
private extern static int SHGetImageList(int iImageList, ref Guid riid, ref IImageList ppv);
```

## VB Signature:
```cs
Declare Function SHGetImageList Lib "shell32.dll" (ByVal iImageList As Long, ByRef riid As Long, ByRef ppv As Any) As Long
Declare Function SHGetImageListXP Lib "shell32.dll" Alias "#727" (ByVal iImageList As Long, ByRef riid As Long, ByRef ppv As Any) As Long
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct RECT
    {
    public int left, top, right, bottom;
    }

    [StructLayout(LayoutKind.Sequential)]
    private struct POINT
    {
    int x;
    int y;
    }

    [StructLayout(LayoutKind.Sequential)]
    private struct IMAGELISTDRAWPARAMS
    {
    public int cbSize;
    public IntPtr himl;
    public int i;
    public IntPtr hdcDst;
    public int x;
    public int y;
    public int cx;
    public int cy;
    public int xBitmap;    // x offest from the upperleft of bitmap
    public int yBitmap;    // y offset from the upperleft of bitmap
    public int rgbBk;
    public int rgbFg;
    public int fStyle;
    public int dwRop;
    public int fState;
    public int Frame;
    public int crEffect;
    }

    [StructLayout(LayoutKind.Sequential)]
    private struct IMAGEINFO
    {
    public IntPtr hbmImage;
    public IntPtr hbmMask;
    public int Unused1;
    public int Unused2;
    public RECT rcImage;
    }
    [ComImportAttribute()]
    [GuidAttribute("46EB5926-582E-4017-9FDF-E8998DAA0950")]
    [InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
    interface IImageList
    {
        [PreserveSig]
        int Add(
        IntPtr hbmImage,
        IntPtr hbmMask,
        ref int pi);

        [PreserveSig]
        int ReplaceIcon(
        int i,
        IntPtr hicon,
        ref int pi);

        [PreserveSig]
        int SetOverlayImage(
        int iImage,
        int iOverlay);

        [PreserveSig]
        int Replace(
        int i,
        IntPtr hbmImage,
        IntPtr hbmMask);

        [PreserveSig]
        int AddMasked(
        IntPtr hbmImage,
        int crMask,
        ref int pi);

        [PreserveSig]
        int Draw(
        ref IMAGELISTDRAWPARAMS pimldp);

        [PreserveSig]
            int Remove(
        int i);

        [PreserveSig]
        int GetIcon(
        int i,
        int flags,
        ref IntPtr picon);

        [PreserveSig]
        int GetImageInfo(
        int i,
        ref IMAGEINFO pImageInfo);

        [PreserveSig]
        int Copy(
        int iDst,
        IImageList punkSrc,
        int iSrc,
        int uFlags);

        [PreserveSig]
        int Merge(
        int i1,
        IImageList punk2,
        int i2,
        int dx,
        int dy,
        ref Guid riid,
        ref IntPtr ppv);

        [PreserveSig]
        int Clone(
        ref Guid riid,
        ref IntPtr ppv);

        [PreserveSig]
        int GetImageRect(
        int i,
        ref RECT prc);

        [PreserveSig]
        int GetIconSize(
        ref int cx,
        ref int cy);

        [PreserveSig]
        int SetIconSize(
        int cx,
        int cy);

        [PreserveSig]
            int GetImageCount(
        ref int pi);

        [PreserveSig]
        int SetImageCount(
        int uNewCount);

        [PreserveSig]
        int SetBkColor(
        int clrBk,
        ref int pclr);

        [PreserveSig]
        int GetBkColor(
        ref int pclr);

        [PreserveSig]
        int BeginDrag(
        int iTrack,
        int dxHotspot,
        int dyHotspot);

        [PreserveSig]
        int EndDrag();

        [PreserveSig]
        int DragEnter(
        IntPtr hwndLock,
        int x,
        int y);

        [PreserveSig]
        int DragLeave(
        IntPtr hwndLock);

        [PreserveSig]
        int DragMove(
        int x,
        int y);

        [PreserveSig]
        int SetDragCursorImage(
        ref IImageList punk,
        int iDrag,
        int dxHotspot,
        int dyHotspot);

        [PreserveSig]
        int DragShowNolock(
        int fShow);

        [PreserveSig]
        int GetDragImage(
        ref POINT ppt,
        ref POINT pptHotspot,
        ref Guid riid,
        ref IntPtr ppv);

        [PreserveSig]
        int GetItemFlags(
        int i,
        ref int dwFlags);

        [PreserveSig]
        int GetOverlayImage(
        int iOverlay,
        ref int piIndex);
    };
```
