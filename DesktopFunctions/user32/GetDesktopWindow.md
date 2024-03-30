
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = false)]
static extern IntPtr GetDesktopWindow();
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=False)> _
Private Shared Function GetDesktopWindow() As IntPtr
End Function
```

## VB Signature:
```cs
Private Declare Auto Function GetDesktopWindow Lib "user32.dll" () As IntPtr
```

## Sample Code:
```cs
Private Declare Auto Function GetDesktopWindow Lib "user32.dll" () As IntPtr

    Private Declare Auto Function GetWindowDC Lib "user32.dll" (ByVal windowHandle As IntPtr) As IntPtr

    Private Declare Auto Function ReleaseDC Lib "user32.dll" (ByVal _
    windowHandle As IntPtr, ByVal dc As IntPtr) As Integer

    Private Declare Auto Function BitBlt Lib "gdi32.dll" (ByVal _
    hdcDest As IntPtr, ByVal nXDest As Integer, ByVal _
    nYDest As Integer, ByVal nWidth As Integer, ByVal _
    nHeight As Integer, ByVal hdcSrc As IntPtr, ByVal nXSrc _
    As Integer, ByVal nYSrc As Integer, ByVal dwRop As _
    System.Int32) As Boolean

    Private Const SRCCOPY As Integer = &HCC0020

    Public Function GetScreenshot(ByVal windowHandle As IntPtr, _
    ByVal location As Point, ByVal size As Size) As Image

    Dim myImage As Image = New Bitmap(size.Width, size.Height)
    Dim g As Graphics = Graphics.FromImage(myImage)

    Dim destDeviceContext As IntPtr = g.GetHdc
    Dim srcDeviceContext As IntPtr = GetWindowDC(windowHandle)

    BitBlt(destDeviceContext, 0, 0, size.Width, size.Height, _ 
           srcDeviceContext, location.X, location.Y, SRCCOPY)
    ReleaseDC(windowHandle, srcDeviceContext)

    g.ReleaseHdc(destDeviceContext)
    g.Dispose

    Return myImage
    End Function

    'Alternately
    Public Function GetDesktopImage(ByVal loc As System.Drawing.Point, _
                    ByVal area As System.Drawing.Size) _
                    As System.Drawing.Image

      Dim bmp As New Bitmap(area.Width, area.Height)
      Dim g As System.Drawing.Graphics = System.Drawing.Graphics.FromImage(bmp)
      Dim ptScr As System.Drawing.Point = Me.PointToScreen(loc)

      g.CopyFromScreen(loc, New Point(0, 0), area, CopyPixelOperation.SourceCopy)

      'housekeeping
      g.Dispose()

      Return bmp
    End Function
```
