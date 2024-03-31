
## C# Definition:
```cs
[StructLayoutAttribute( LayoutKind.Sequential )]
struct BITMAPINFO {
   /// <summary>
   /// A BITMAPINFOHEADER structure that contains information about the dimensions of color format.
   /// </summary>
   public BITMAPINFOHEADER bmiHeader;

   /// <summary>
   /// An array of RGBQUAD. The elements of the array that make up the color table.
   /// </summary>
   [MarshalAsAttribute( UnmanagedType.ByValArray, SizeConst = 1, ArraySubType = UnmanagedType.Struct )]
   public RGBQUAD[] bmiColors;
}
```

## VB Definition:
```cs
Structure BITMAPINFO 
   Public TODO
End Structure
```
