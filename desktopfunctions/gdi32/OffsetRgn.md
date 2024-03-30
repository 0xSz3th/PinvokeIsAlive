
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int OffsetRgn(IntPtr hrgn, int nXOffset, int nYOffset);
```

## Sample Code:
```cs
With tmpForm
    If .BorderStyle <> 0 Then
        Dim xoff As Long, yoff As Long

        .ScaleMode = vbPixels

        xoff = (.ScaleX(.Width, vbTwips, vbPixels) - .ScaleWidth) / 2
        yoff = .ScaleY(.Height, vbTwips, vbPixels) - .ScaleHeight - xoff

        Call OffsetRgn(hndRegion, xoff, yoff)
    End If
    End With
```
