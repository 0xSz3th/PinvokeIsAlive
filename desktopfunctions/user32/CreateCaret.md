
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool CreateCaret(IntPtr hWnd, IntPtr hBitmap, int nWidth,
   int nHeight);
```

## VB.NET:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
    Public Shared Function CreateCaret(ByVal hWnd As IntPtr, ByVal hBitmap As IntPtr, ByVal nWidth As Integer, ByVal nHeight As Integer) As Boolean
    End Function
```

## Tips & Tricks:
```cs
int r = CursorColour.R ^ ParentControl.BackColor.R;
    int g = CursorColour.G ^ ParentControl.BackColor.G;
    int b = CursorColour.B ^ ParentControl.BackColor.B;
```

## Sample Code:
```cs
private void button1_Click(object sender, System.EventArgs e) {
        CreateCaret(textBox1.Handle, IntPtr.Zero, 0, textBox1.Height);
        ShowCaret(textBox1.Handle);
    }
```

## Sample Code:
```cs
<DllImport("user32.dll", SetLastError:=True)> 
    Public Shared Function CreateCaret(ByVal hWnd As IntPtr, ByVal hBitmap As IntPtr, ByVal nWidth As Integer, ByVal nHeight As Integer) As Boolean
    End Function

    Private Sub TextBox1_GotFocus(sender As Object, e As EventArgs) Handles TextBox1.GotFocus
    HideCaret(TextBox1.Handle)
    Dim bmPtr As IntPtr = GetHBitmap()
    CreateCaret(TextBox1.Handle, bmPtr, 2, 12)
    SetCaretBlinkTime(300)
    ShowCaret(TextBox1.Handle)
    End Sub
```

## Sample Code:
```cs
The hBitmap parameter is a handle to the bitmap you want to use(or gray/solid).

    You can use the following to specify if you want gray/solid:

    Public Class hBMParameters
    Public Shared Property Gray As IntPtr = CType(1, IntPtr)
    Public Shared Property Solid As IntPtr = Nothing
    End Class
```

## Sample Code:
```cs
Bitmaps have a method attached to return the handle

    Example:  
    Function GetHBitmap() As IntPtr
    Dim embeddedBitmap As Byte() = {137, 80, 78, 71, 13, 10, 26, 10, 0, 0, 0, 13, 73, 72, 68, 82, 0, 0, 0, 10, 0, 0, 0, 10, 8, 2, 0, 0, 0, 2, 80, 88, 234, 0, 0, 0, 1, 115, 82, 71, 66, 0, 174, 206, 28, 233, 0, 0, 0, 4, 103, 65, 77, 65, 0, 0, 177, 143, 11, 252, 97, 5, 0, 0, 0, 9, 112, 72, 89, 115, 0, 0, 14, 195, 0, 0, 14, 195, 1, 199, 111, 168, 100, 0, 0, 0, 48, 73, 68, 65, 84, 40, 83, 99, 248, 143, 23, 16, 39, 205, 192, 128, 162, 14, 206, 165, 138, 225, 184, 0, 204, 14, 252, 118, 3, 249, 8, 33, 100, 54, 132, 2, 2, 136, 40, 4, 64, 133, 144, 165, 177, 128, 255, 255, 1, 57, 41, 7, 8, 21, 108, 65, 188, 0, 0, 0, 0, 73, 69, 78, 68, 174, 66, 96, 130}
    Dim bm As Bitmap
    Using s As New System.IO.MemoryStream(embeddedBitmap)
        bm = CType(Bitmap.FromStream(s), Bitmap)
    End Using
    Return bm.GetHbitmap()
    End Function
```
