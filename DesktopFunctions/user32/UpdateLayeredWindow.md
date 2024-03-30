
## C# Signature:
```cs
[DllImport("user32.dll", ExactSpelling = true, SetLastError = true)]
static extern bool UpdateLayeredWindow(IntPtr hwnd, IntPtr hdcDst,
   ref Point pptDst, ref Size psize, IntPtr hdcSrc, ref Point pptSrc, uint crKey,
   [In] ref BLENDFUNCTION pblend, uint dwFlags);
```

## Tips & Tricks:
```cs
public void SetBackground(Control control, Bitmap bitmap)
    {
        /*Parametri accettati dalla procedura:
        control = il form o controllo da renderizzare
        bitmap = la PNG da utilizzare come sfondo*/

        // Imposta le dimensioni del controllo come quelle della bitmap
        control.Width = bitmap.Width;
        control.Height = bitmap.Height;
        if (bitmap.PixelFormat != System.Drawing.Imaging.PixelFormat.Format32bppArgb)
        {
            //Se l'immagine è in formato errato...
            throw new ApplicationException("L'immagine deve essere in formato a 32 bpp con canale alpha");
        }
        IntPtr hBitmap = IntPtr.Zero;
        IntPtr oldBitmap = IntPtr.Zero;
        IntPtr screenDc = Win32.GetDC(IntPtr.Zero);
        IntPtr memDc = Win32.CreateCompatibleDC(screenDc);
        try
        {
            hBitmap = bitmap.GetHbitmap(Color.FromArgb(0));
            oldBitmap = Win32.SelectObject(memDc, hBitmap);
            Win32.Size size = new Win32.Size(bitmap.Width, bitmap.Height);
            Win32.Point pointSource = new Win32.Point(control.Left, control.Top);
            Win32.Point topPos = new Win32.Point(0, 0);
            Win32.BLENDFUNCTION blend = new Win32.BLENDFUNCTION();
            blend.BlendOp = 0;
            blend.BlendFlags = 0;
            blend.SourceConstantAlpha = byte.MaxValue;
            blend.AlphaFormat = 1;
            Win32.UpdateLayeredWindow(control.Handle, screenDc, ref topPos, ref size, memDc, ref pointSource, 0, ref blend, 2);
        }
        catch (Exception ex)
        {
            throw ex;
        }
        finally
        {
            Win32.ReleaseDC(IntPtr.Zero, screenDc);            
            if (hBitmap != IntPtr.Zero)
            {
                Win32.SelectObject(memDc, oldBitmap);
                Win32.DeleteObject(hBitmap);
            }
            Win32.DeleteDC(memDc);
        }
    }    

    public class Win32
    {
        //Classe che contiene le dichiarazioni API e i tipi
        public enum Bool: int
        {
            @False = 0,

            @True = 1

        }

        public struct Point
        {
            public int x;

            public int y;


            public Point(int x, int y)
            {
                this.x = x;
                this.y = y;
            }
        }

        public struct Size
        {
            public int cx;

            public int cy;


            public Size(int cx, int cy)
            {
                this.cx = cx;
                this.cy = cy;
            }
        }

        public struct BLENDFUNCTION
        {
            public byte BlendOp;

            public byte BlendFlags;

            public byte SourceConstantAlpha;

            public byte AlphaFormat;

        }

        public const int ULW_ALPHA = 2;

        public const byte AC_SRC_OVER = 0;

        public const byte AC_SRC_ALPHA = 1;
```

## Tips & Tricks:
```cs
[DllImportAttribute("user32.dll")]
        public extern static Bool UpdateLayeredWindow(IntPtr handle, IntPtr hdcDst, ref Point pptDst, ref Size psize, IntPtr hdcSrc, ref Point pprSrc, int crKey, ref BLENDFUNCTION pblend, int dwFlags);

        [DllImportAttribute("user32.dll")]
        public extern static IntPtr GetDC(IntPtr handle);

        [DllImportAttribute("user32.dll", ExactSpelling=true)]
        public extern static int ReleaseDC(IntPtr handle, IntPtr hDC);

        [DllImportAttribute("gdi32.dll")]
        public extern static IntPtr CreateCompatibleDC(IntPtr hDC);

        [DllImportAttribute("gdi32.dll")]
        public extern static Bool DeleteDC(IntPtr hdc);

        [DllImportAttribute("gdi32.dll")]
        public extern static IntPtr SelectObject(IntPtr hDC, IntPtr hObject);

        [DllImportAttribute("gdi32.dll")]
        public extern static Bool DeleteObject(IntPtr hObject);
    }
```
