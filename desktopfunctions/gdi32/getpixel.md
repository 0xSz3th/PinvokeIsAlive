
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern uint GetPixel(IntPtr hdc, int nXPos, int nYPos);
```

## VB.NET Signature
```cs
<DllImport("gdi32.dll", SetLastError:=True)> _
Public Function GetPixel(hdc As IntPtr, _
              nXPos As Integer, _
              nYPos as Integer) As UInteger
End Function
```

## VB Signature:
```cs
Public Declare Function GetPixel Lib "gdi32" Alias "GetPixel" (ByVal hdc As Long, ByVal X As Long, ByVal Y As Long) As Long
```

## Alternative Managed API:
```cs
using (Bitmap bmp = new Bitmap(Screen.PrimaryScreen.Bounds.Width,
                   Screen.PrimaryScreen.Bounds.Height, 
                   PixelFormat.Format32bppArgb)) 
    {
    using (Graphics g = Graphics.FromImage(bmp)) 
    {
        g.CopyFromScreen(Screen.PrimaryScreen.Bounds.X,
                 Screen.PrimaryScreen.Bounds.Y, 
                 0, 0, 
                 Screen.PrimaryScreen.Bounds.Size, 
                 CopyPixelOperation.SourceCopy);
    }
    return bmp.GetPixel(x, y);
    }
```

## Sample Code:
```cs
[DllImport("user32.dll")]
  static extern IntPtr GetDC(IntPtr hwnd);

  [DllImport("user32.dll")]
  static extern Int32 ReleaseDC(IntPtr hwnd, IntPtr hdc);

  [DllImport("gdi32.dll")]
  static extern uint GetPixel(IntPtr hdc,int nXPos,int nYPos);

  // Print out the RGB value of the pixel which is under the mouse cursor.
  // NB: BLUE and RED components will be swapped because GetPixel returns ABGR
  static private void myControl_MouseMove(object sender,System.Windows.Forms.MouseEventArgs e)
  {
    IntPtr hdc = GetDC(IntPtr.Zero);
    uint pixel = GetPixel(hdc, Cursor.Position.X, Cursor.Position.Y);
    ReleaseDC(IntPtr.Zero,hdc);
    Color color = Color.FromArgb((int)pixel);
    Console.WriteLine("Color is {0}",color);
  }
```

## 2nd Example (above did not work for me, here is my solution):
```cs
[DllImport("gdi32.dll")]
    static extern IntPtr CreateDC(string strDriver,
      string strDevice, string strOutput, IntPtr pData);

    [DllImport("gdi32.dll")]
    static extern bool DeleteDC(IntPtr hdc);

    [DllImport("gdi32.dll")]
    static extern int GetPixel(IntPtr hdc, int nXPos, int nYPos);

    // ...
    IntPtr hdcScreen = CreateDC("Display", null, null, IntPtr.Zero);
    int cr = GetPixel(hdcScreen, x, y);
    Color color = Color.FromArgb((cr & 0x000000FF),
        (cr & 0x0000FF00) >> 8,
        (cr & 0x00FF0000) >> 16);
    DeleteDC(hdcScreen);
    // ... and apply the color to Bitmap-struct via SetPixel() or whatever else you want to do with it..
```

## Wrapper Class
```cs
using System;
  using System.Drawing;
  using System.Runtime.InteropServices;

  sealed class Win32
  {
      [DllImport("user32.dll")]
      static extern IntPtr GetDC(IntPtr hwnd);

      [DllImport("user32.dll")]
      static extern Int32 ReleaseDC(IntPtr hwnd, IntPtr hdc);

      [DllImport("gdi32.dll")]
      static extern uint GetPixel(IntPtr hdc, int nXPos, int nYPos);

      static public System.Drawing.Color GetPixelColor(int x, int y)
      {
       IntPtr hdc = GetDC(IntPtr.Zero);
       uint pixel = GetPixel(hdc, x, y);
       ReleaseDC(IntPtr.Zero, hdc);
       Color color = Color.FromArgb((int)(pixel & 0x000000FF),
                    (int)(pixel & 0x0000FF00) >> 8,
                    (int)(pixel & 0x00FF0000) >> 16);
       return color;
      }
   }
```
