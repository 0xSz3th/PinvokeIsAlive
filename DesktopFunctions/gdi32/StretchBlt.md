
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool StretchBlt(IntPtr hdcDest, int nXOriginDest, int nYOriginDest, 
    int nWidthDest, int nHeightDest, 
    IntPtr hdcSrc, int nXOriginSrc, int nYOriginSrc, int nWidthSrc, int nHeightSrc,     
    TernaryRasterOperations dwRop );
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> _
Private Shared Function StretchBlt(hdcDest As IntPtr, nXOriginDest As Integer, nYOriginDest As Integer, nWidthDest As Integer, nHeightDest As Integer, hdcSrc As IntPtr, nXOriginSrc As Integer, nYOriginSrc As Integer, nWidthSrc As Integer, nHeightSrc As Integer, dwRop As TernaryRasterOperations) As Boolean
End Function
```

## Sample Code:
```cs
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.Runtime.InteropServices;

namespace StretchBlt_with_bitmap_image
{
    /// <summary>
    /// Summary description for Form1.
    /// </summary>
    public class Form1 : System.Windows.Forms.Form
    {
        /// <summary>
        /// Required designer variable.
        /// </summary>
        private System.ComponentModel.Container components = null;

        Bitmap bmp;
        private System.Windows.Forms.MainMenu mainMenu1;
        private System.Windows.Forms.MenuItem menuItem1;
        private System.Windows.Forms.MenuItem menuItem2;

        IntPtr hbmp;

        public Form1()
        {
            InitializeComponent();            
        }

        /// <summary>
        /// Clean up any resources being used.
        /// </summary>
        protected override void Dispose( bool disposing )
        {
            if( disposing )
            {
                if (components != null) 
                {
                    components.Dispose();
                }
            }
            base.Dispose( disposing );
        }

        #region Windows Form Designer generated code
        /// <summary>
        /// Required method for Designer support - do not modify
        /// the contents of this method with the code editor.
        /// </summary>
        private void InitializeComponent()
        {
            this.mainMenu1 = new System.Windows.Forms.MainMenu();
            this.menuItem1 = new System.Windows.Forms.MenuItem();
            this.menuItem2 = new System.Windows.Forms.MenuItem();
            // 
            // mainMenu1
            // 
            this.mainMenu1.MenuItems.AddRange(new System.Windows.Forms.MenuItem[] {
                                                                                      this.menuItem1});
            // 
            // menuItem1
            // 
            this.menuItem1.Index = 0;
            this.menuItem1.MenuItems.AddRange(new System.Windows.Forms.MenuItem[] {
                                                                                      this.menuItem2});
            this.menuItem1.Text = "Fie";
            // 
            // menuItem2
            // 
            this.menuItem2.Index = 0;
            this.menuItem2.Text = "open";
            this.menuItem2.Click += new System.EventHandler(this.menuItem2_Click);
            // 
            // Form1
            // 
            this.AutoScaleBaseSize = new System.Drawing.Size(5, 13);
            this.ClientSize = new System.Drawing.Size(292, 273);
            this.Menu = this.mainMenu1;
            this.Name = "Form1";
            this.Text = "Form1";
            this.Paint += new System.Windows.Forms.PaintEventHandler(this.Form1_Paint);

        }
        #endregion

        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main() 
        {
            Application.Run(new Form1());
        }

        private void Form1_Paint(object sender, System.Windows.Forms.PaintEventArgs e)
        {
            if(bmp != null)
            {
                this.AutoScrollMinSize = bmp.Size;
                hbmp = bmp.GetHbitmap();

                IntPtr pTarget = e.Graphics.GetHdc();
                IntPtr pSource = CreateCompatibleDC(pTarget);
                IntPtr pOrig = SelectObject(pSource, hbmp);

                StretchBlt(pTarget, this.AutoScrollPosition.X,
                    this.AutoScrollPosition.Y,  bmp.Width , bmp.Height ,pSource,  
                    0,0,bmp.Width,  bmp.Height,TernaryRasterOperations.SRCCOPY);

                IntPtr pNew = SelectObject(pSource, pOrig);
                DeleteObject(pNew);
                DeleteDC(pSource);
                e.Graphics.ReleaseHdc(pTarget);
            }
        }

        private void Form1_Resize(object sender, System.EventArgs e)
        {
            this.Invalidate();
        }

        string _fileName = "";

        //File open click
        private void menuItem2_Click(object sender, System.EventArgs e)
        {
            OpenFileDialog dlg = new OpenFileDialog();

            if(dlg.ShowDialog() == DialogResult.OK)
            {
                _fileName = dlg.FileName;
            }
            bmp = new Bitmap(_fileName);
            this.AutoScrollMinSize = bmp.Size;
            this.Invalidate();
        }

        [DllImport("gdi32.dll")]
        static extern bool StretchBlt(IntPtr hdcDest, int nXOriginDest,
            int nYOriginDest, int nWidthDest, int nHeightDest, IntPtr hdcSrc,
            int nXOriginSrc, int nYOriginSrc, int nWidthSrc, int nHeightSrc,     
            TernaryRasterOperations dwRop );
```

## Sample Code:
```cs
[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
        static extern IntPtr CreateCompatibleDC(IntPtr hdc);
```

## Sample Code:
```cs
[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
        static extern bool DeleteDC(IntPtr hdc);
```

## Sample Code:
```cs
[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
        static extern IntPtr SelectObject(IntPtr hdc, IntPtr hgdiobj);
```

## Sample Code:
```cs
[DllImport("gdi32.dll", ExactSpelling=true, SetLastError=true)]
        static extern bool DeleteObject(IntPtr hObject);
```

## Sample Code:
```cs
[DllImport("gdi32.dll")]
        static extern bool SetStretchBltMode(IntPtr hdc, StretchMode iStretchMode);
```

## Sample Code:
```cs
public enum StretchMode
        {
            STRETCH_ANDSCANS    =1,
            STRETCH_ORSCANS     =2,
            STRETCH_DELETESCANS =3,
            STRETCH_HALFTONE    =4,
        }
```

## Sample Code:
```cs
public enum TernaryRasterOperations
        {
            SRCCOPY     = 0x00CC0020, /* dest = source*/
            SRCPAINT    = 0x00EE0086, /* dest = source OR dest*/
            SRCAND      = 0x008800C6, /* dest = source AND dest*/
            SRCINVERT   = 0x00660046, /* dest = source XOR dest*/
            SRCERASE    = 0x00440328, /* dest = source AND (NOT dest )*/
            NOTSRCCOPY  = 0x00330008, /* dest = (NOT source)*/
            NOTSRCERASE = 0x001100A6, /* dest = (NOT src) AND (NOT dest) */
            MERGECOPY   = 0x00C000CA, /* dest = (source AND pattern)*/
            MERGEPAINT  = 0x00BB0226, /* dest = (NOT source) OR dest*/
            PATCOPY     = 0x00F00021, /* dest = pattern*/
            PATPAINT    = 0x00FB0A09, /* dest = DPSnoo*/
            PATINVERT   = 0x005A0049, /* dest = pattern XOR dest*/
            DSTINVERT   = 0x00550009, /* dest = (NOT dest)*/
            BLACKNESS   = 0x00000042, /* dest = BLACK*/
            WHITENESS   = 0x00FF0062, /* dest = WHITE*/
        };
    }
}
```
