
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr GetWindowDC(IntPtr hWnd);
```

## VB.NET Signature:
```cs
<DllImport("User32.dll")> _
Public Shared Function GetWindowDC(ByVal hWnd As IntPtr) As IntPtr
End Function
```

## VB Signature:
```cs
Declare Function GetWindowDC Lib "user32" (ByVal hWnd As Long) As Long
```

## Sample Code:
```cs
Private Declare Auto Function BitBlt Lib "gdi32.dll" (ByVal hdcDest As IntPtr, ByVal nXDest As Integer, ByVal _
    nYDest As Integer, ByVal nWidth As Integer, ByVal nHeight As Integer, ByVal hdcSrc As IntPtr, ByVal nXSrc _
    As Integer, ByVal nYSrc As Integer, ByVal dwRop As System.Int32) As Boolean
  Private Const SRCCOPY As Integer = &HCC0020
  Declare Function GetWindowDC Lib "user32" (ByVal hwnd As IntPtr) As IntPtr

  ' Get an image of the form plus its decoration
  ' (borders, title bar, etc).
  Private Function GetDecoratedFormImage() As Bitmap
    ' Get this form's Graphics object.
    Dim MyGrph As Graphics = Me.CreateGraphics

    ' Make a Bitmap to hold the image.
    Dim TempBMP As New Bitmap(Me.Width, Me.Height, MyGrph)
    Dim MyGrphBmp As Graphics = MyGrph.FromImage(TempBMP)
    Dim MyGrphBmpHdc As IntPtr = MyGrphBmp.GetHdc

    ' Get the form's hDC. We must do this after 
    ' creating the new Bitmap, which uses me_gr.
    Dim MyGrphHdc As IntPtr = GetWindowDC(Me.Handle)

    ' BitBlt the form's image onto the Bitmap.
    BitBlt(MyGrphBmpHdc, 0, 0, Me.Width, Me.Height, MyGrphHdc, 0, 0, SRCCOPY)
    MyGrphBmp.ReleaseHdc(MyGrphBmpHdc)

    ' Return the result.
    Return TempBMP
  End Function
```
