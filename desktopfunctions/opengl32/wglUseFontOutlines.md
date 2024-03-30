
## C# Signature:
```cs
[DllImport("opengl32", EntryPoint = "wglUseFontOutlines", CallingConvention=CallingConvention.Winapi)]
public static extern bool wglUseFontOutlines(
IntPtr hDC,
[MarshalAs(UnmanagedType.U4)] UInt32 first,
[MarshalAs(UnmanagedType.U4)] UInt32 count,
[MarshalAs(UnmanagedType.U4)] UInt32 listBase,
[MarshalAs(UnmanagedType.R4)] Single deviation,
[MarshalAs(UnmanagedType.R4)] Single extrusion,
[MarshalAs(UnmanagedType.I4)] Int32 format,
[Out] Gdi.GLYPHMETRICSFLOAT[] lpgmf);

[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
public struct GLYPHMETRICSFLOAT 
{
    public Single      gmfBlackBoxX;
    public Single      gmfBlackBoxY;
    public POINTFLOAT  gmfptGlyphOrigin;
    public Single      gmfCellIncX;
    public Single      gmfCellIncY;
}

public struct POINTFLOAT
{
    public Single      x;
    public Single      y;
}
```

## VB Signature:
```cs
Declare Function wglUseFontOutlines Lib "opengl32.dll" (TODO) As TODO
```

## Sample Code:
```cs
public Gdi.GLYPHMETRICSFLOAT[] gmf = null;
        public UInt32 FontBase = 0;
        IntPtr _OldFontH = IntPtr.Zero;
        public void Individual_OpenGLInit( System.Windows.Forms.PaintEventArgs pe )
        {
            #region Generate GDI WGL FONT OUTLINES

            try
            {
                gmf = new Gdi.GLYPHMETRICSFLOAT[256];

                IntPtr dc = pe.Graphics.GetHdc();
                System.Drawing.Font font =
                    new Font(
                    "Verdana",
                    9F,
                    System.Drawing.FontStyle.Regular,
                    System.Drawing.GraphicsUnit.Point,
                    ((System.Byte)(0)));

                FontBase = GL.glGenLists(256);

                IntPtr fontH = font.ToHfont();
                _OldFontH = Gdi.SelectObject(dc, fontH);

                WGL.wglUseFontOutlines(
                    dc,
                    0,
                    255,
                    FontBase,
                    0,
                    0.2f,
                    WGL.WGL_FONT_POLYGONS,
                    gmf);

                pe.Graphics.ReleaseHdc(dc);
            }
            catch
            {
                Console.Error.WriteLine("Unable to initialize fonts [FAILED]");
            }

            #endregion
        }

        public void Individual_OpenGLDeinit( System.Windows.Forms.PaintEventArgs pe )
        {
            #region Deinit GDI WGL FONT OUTLINES

            try
            {
                if(gmf != null)
                    gmf = null;

                IntPtr dc = pe.Graphics.GetHdc();
                IntPtr disposeFontH = Gdi.SelectObject(dc, _OldFontH);
                Gdi.DeleteObject(disposeFontH);
                GL.glDeleteLists(FontBase, 256);
                pe.Graphics.ReleaseHdc(dc);
            }
            catch
            {
                Console.Error.WriteLine("Unable to de-initialize fonts [FAILED]");
            }

            #endregion
        }

        public void glPrint(String outputString,Int32 x1, Int32 y1, Int32 x2,
            Int32 y2)
        {
            if(outputString == null)
                return;

            if(outputString.Length == 0)
                return;

            GL.glPushMatrix();            

            Single scale = 15.0f;

            GL.glMatrixMode(GL.GL_MODELVIEW);
            GL.glTranslatef(x1,y1,0);
            GL.glScalef(scale, -scale, scale);

            GL.glPushAttrib(GL.GL_LIST_BIT);
            GL.glListBase(m_Parent.m_TagcWorkspaceControl.FontBase);

            // Find width of string
            Int32 i=0;
            float width = 0;
            for( ; i<outputString.Length; i++)
            {
                width +=
                    m_Parent.m_TagcWorkspaceControl.gmf[ outputString[i] ] . 
                    gmfCellIncX * scale;
                if((x1+width)>=x2)
                    break;
                if((y1+
                    m_Parent.m_TagcWorkspaceControl.gmf[ outputString[i] ] . 
                    gmfCellIncY * scale)>=y2)
                    break;
            }

            // Print the string if there is room
            if(i>0)
                GL.glCallLists(i, GL.GL_UNSIGNED_BYTE, outputString);
            GL.glPopAttrib();

            GL.glPopMatrix();
        }

        public Int32 getPrintWidth(String outputString)
        {
            if(outputString == null)
                return 0;

            if(outputString.Length == 0)
                return 0;

            Single scale = 15.0f;

            // Find width of string
            float width = 0;
            for(Int32 i=0; i<outputString.Length; i++)
            {
                width +=
                    m_Parent.m_TagcWorkspaceControl.gmf[ outputString[i] ] . 
                    gmfCellIncX * scale;
            }

            return (Int32)Math.Ceiling(width);
        }
```
