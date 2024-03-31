
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct BITMAPINFOHEADER
{
    public uint  biSize; 
    public int   biWidth; 
    public int   biHeight; 
    public ushort   biPlanes; 
    public ushort   biBitCount; 
    public BitmapCompressionMode  biCompression; 
    public uint  biSizeImage; 
    public int   biXPelsPerMeter; 
    public int   biYPelsPerMeter; 
    public uint  biClrUsed; 
    public uint  biClrImportant; 

    public void Init()
    {
        biSize = (uint)Marshal.SizeOf(this);
    }
}
```

## VB Definition:
```cs
Public Structure BITMAPINFOHEADER
     Public biSize As Int32
     Public biWidth As Int32
     Public biHeight As Int32
     Public biPlanes As Int16
     Public biBitCount As Int16
     Public biCompression As BitmapCompressionMode
     Public biSizeImage As Int32
     Public biXPelsperMeter As Int32
     Public biYPelsPerMeter As Int32
     Public biClrUsed As Int32
     Public biClrImportant As Int32
End Structure
```
