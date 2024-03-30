
## C# Signature:
```cs
[DllImport("Kernel32.dll", EntryPoint="RtlMoveMemory", SetLastError=false)]
static extern void MoveMemory(IntPtr dest, IntPtr src, int size);
```

## VB Signature:
```cs
Declare Auto Sub MoveMemory Lib "Kernel32.dll" _
    Alias "RtlMoveMemory" (ByVal dest As IntPtr, ByVal src As IntPtr, ByVal size As Integer)
```

## VBA Signature:
```cs
Private Declare PtrSafe Function MoveMemory Lib "KERNEL32.dll" _
    Alias "RtlMoveMemory" (ByVal dest As LongPtr, ByVal src As LongPtr, ByVal size As Integer)
```

## Sample Code:
```cs
Dim nColors As Integer = 2
  Select Case nColors
    Case nColors > 256
      nColors = 256
    Case nColors < 2
      nColors = 2
  End Select
  Dim Width As Integer = pSrcImg.Width
  Dim Height As Integer = pSrcImg.Height
  Dim bitmap As Bitmap = New Bitmap(Width, Height, PixelFormat.Format1bppIndexed)
  Dim BmpCopy As Bitmap = New Bitmap(Width, Height, PixelFormat.Format32bppArgb)
  Dim g As Graphics
  g = Graphics.FromImage(BmpCopy)
  g.PageUnit = GraphicsUnit.Pixel
  g.DrawImage(pSrcImg, 0, 0, Width, Height)
  g.Dispose()
  Dim bitmapData As BitmapData
  Dim rect As Rectangle = New Rectangle(0, 0, Width, Height)
  bitmapData = bitmap.LockBits(rect, ImageLockMode.WriteOnly, PixelFormat.Format1bppIndexed)
  Dim pixels As IntPtr = bitmapData.Scan0
  Dim bits As Byte()
  Dim pBits As Int32
  If (bitmapData.Stride > 0) Then
    pBits = pixels.ToInt32()
  Else
    pBits = pixels.ToInt32() + bitmapData.Stride * (Height - 1)
  End If
  Dim stride As Integer = Math.Abs(bitmapData.Stride)
  ReDim bits(Height * stride) ' Allocate the working buffer.
  Dim row As Integer
  Dim col As Integer
  Dim bmask As Integer
  For row = 0 To Height - 1
    For col = 0 To Width - 1
      Dim pixel As Color ' The source pixel.
      Dim i8BppPixel As Integer = (row * stride) + Int(col / 8)
      bmask = &H80 / (2 ^ (col Mod 8))
      pixel = BmpCopy.GetPixel(col, row)
      Dim luminance As Double = (pixel.R * 0.299) + (pixel.G * 0.587) + (pixel.B * 0.114)
      Dim colorIndex As Double = Math.Round((luminance * (nColors - 1) / 255))
      If colorIndex = 0 Then
    bits(i8BppPixel) = bits(i8BppPixel) Or (bmask And 0) 'Black
      Else
    bits(i8BppPixel) = bits(i8BppPixel) Or (bmask Or 0) 'White
      End If
    Next col
  Next row
  CopyArrayTo(pBits, bits, Height * stride)
  bitmap.UnlockBits(bitmapData)
  BmpCopy.Dispose()
  Return bitmap
```
