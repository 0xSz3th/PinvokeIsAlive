
## C# Signature:
```cs
/// <summary>
///        Creates a bitmap compatible with the device that is associated with the specified device context.
/// </summary>
/// <param name="hdc">A handle to a device context.</param>
/// <param name="nWidth">The bitmap width, in pixels.</param>
/// <param name="nHeight">The bitmap height, in pixels.</param>
/// <returns>If the function succeeds, the return value is a handle to the compatible bitmap (DDB). If the function fails, the return value is <see cref="System.IntPtr.Zero"/>.</returns>
[DllImport("gdi32.dll", EntryPoint = "CreateCompatibleBitmap")]
static extern IntPtr CreateCompatibleBitmap([In] IntPtr hdc, int nWidth, int nHeight);
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> _
Private Shared Function CreateCompatibleBitmap(hdc As IntPtr, nWidth As Integer, nHeight As Integer) As IntPtr
End Function
```
