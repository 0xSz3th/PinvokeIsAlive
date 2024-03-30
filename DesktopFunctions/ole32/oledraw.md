
## C# Signature:
```cs
[DllImport("ole32.dll")]
       static extern int OleDraw([MarshalAs(UnmanagedType.IUnknown)] object pUnk,
      uint dwAspect, IntPtr hdcDraw, [In] ref RECT lprcBounds);
```

## Sample Code:
```cs
[DllImport("ole32.dll")]
       public static extern int OleDraw(IntPtr pUnk, int dwAspect, IntPtr hdcDraw, ref Rectangle lprcBounds);

       /// <summary>
       /// Creates a bitmap from the supplied ActiveX control using OleDraw
       /// </summary>
       /// <param name="c"></param>
       public Image CreateImage(AxHost c)
       {
           Rectangle rect = new Rectangle(0,
                          0,
                          c.ClientRectangle.Width,
                          c.ClientRectangle.Height);

           Bitmap bmp = new Bitmap(rect.Width, rect.Height);
           Graphics graphics = Graphics.FromImage(bmp);
           IntPtr pUnk = Marshal.GetIUnknownForObject(c.GetOcx());
           IntPtr hdc = graphics.GetHdc();

           OleDraw(pUnk, 1, hdc, ref rect);

           Marshal.Release(pUnk);
           graphics.ReleaseHdc(hdc);

           return bmp;
       }
```
