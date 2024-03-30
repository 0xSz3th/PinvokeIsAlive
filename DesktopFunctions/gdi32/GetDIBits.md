
## C# Signature:
```cs
/// <summary>
///        Retrieves the bits of the specified compatible bitmap and copies them into a buffer as a DIB using the specified format.
/// </summary>
/// <param name="hdc">A handle to the device context.</param>
/// <param name="hbmp">A handle to the bitmap. This must be a compatible bitmap (DDB).</param>
/// <param name="uStartScan">The first scan line to retrieve.</param>
/// <param name="cScanLines">The number of scan lines to retrieve.</param>
/// <param name="lpvBits">A pointer to a buffer to receive the bitmap data. If this parameter is <see cref="IntPtr.Zero"/>, the function passes the dimensions and format of the bitmap to the <see cref="BITMAPINFO"/> structure pointed to by the <paramref name="lpbi"/> parameter.</param>
/// <param name="lpbi">A pointer to a <see cref="BITMAPINFO"/> structure that specifies the desired format for the DIB data.</param>
/// <param name="uUsage">The format of the bmiColors member of the <see cref="BITMAPINFO"/> structure. It must be one of the following values.</param>
/// <returns>If the lpvBits parameter is non-NULL and the function succeeds, the return value is the number of scan lines copied from the bitmap.
/// If the lpvBits parameter is NULL and GetDIBits successfully fills the <see cref="BITMAPINFO"/> structure, the return value is nonzero.
/// If the function fails, the return value is zero.
/// This function can return the following value: ERROR_INVALID_PARAMETER (87 (0×57))</returns>
[DllImport("gdi32.dll", EntryPoint = "GetDIBits")]
static extern int GetDIBits([In] IntPtr hdc, [In] IntPtr hbmp, uint uStartScan, uint cScanLines, [Out] byte[] lpvBits, ref BITMAPINFO lpbi, DIB_Color_Mode uUsage);
```
