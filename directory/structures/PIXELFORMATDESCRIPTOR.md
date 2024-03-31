
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct PixelFormatDescriptor
{
    public ushort Size;
    public ushort Version;
    public PixelFormatDescriptorFlags Flags;
    public PixelType PixelType;
    public byte ColorBits;
    public byte RedBits;
    public byte RedShift;
    public byte GreenBits;
    public byte GreenShift;
    public byte BlueBits;
    public byte BlueShift;
    public byte AlphaBits;
    public byte AlphaShift;
    public byte AccumBits;
    public byte AccumRedBits;
    public byte AccumGreenBits;
    public byte AccumBlueBits;
    public byte AccumAlphaBits;
    public byte DepthBits;
    public byte StencilBits;
    public byte AuxBuffers;
    public byte LayerType;
    private byte Reserved;
    public uint LayerMask;
    public uint VisibleMask;
    public uint DamageMask;

    //Use this function to make a new one with Size and Version already filled in.
    public static PixelFormatDescriptor Build()
    {
    var pfd = new PixelFormatDescriptor
    {
        Size = (ushort)Marshal.SizeOf(typeof(PixelFormatDescriptor)),
        Version = 1
    };

    return pfd;
    }
}
```

## VB Definition:
```cs
Structure PIXELFORMATDESCRIPTOR 
   Public TODO
End Structure
```
