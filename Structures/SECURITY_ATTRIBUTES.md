
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct SECURITY_ATTRIBUTES
{
    public int nLength;
    public unsafe byte* lpSecurityDescriptor;
    public int bInheritHandle;
}
```

## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct SECURITY_ATTRIBUTES
{
    public int nLength;
    public IntPtr lpSecurityDescriptor;
    public int bInheritHandle;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Structure SECURITY_ATTRIBUTES 
   Public nLength As Integer
   Public lpSecurityDescriptor As IntPtr
   Public bInheritHandle As Integer
End Structure
```

##  Sample Code - C# - sivakumar.keerthi
```cs
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.Runtime.InteropServices;
using System.Diagnostics;
using System.Security.AccessControl;

namespace WindowsApplication1
{
    [StructLayout(LayoutKind.Sequential)]
    public struct SECURITY_ATTRIBUTES
    {
        public int nLength;
        public IntPtr lpSecurityDescriptor;
        public int bInheritHandle;
    }

    public class Form1 : System.Windows.Forms.Form
    {
        /// <summary>
        /// Required designer variable.
        /// </summary>
        [DllImport("kernel32.dll")]
        static extern bool CreateDirectory(string lpPathName, SECURITY_ATTRIBUTES lpSecurityAttributes);        
        private System.ComponentModel.Container components = null;

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
            this.SuspendLayout();
            // 
            // Form1
            // 
            this.AutoScaleBaseSize = new System.Drawing.Size(5, 13);
            this.ClientSize = new System.Drawing.Size(528, 266);
            this.Name = "Form1";
            this.Text = "Form1";
            this.Load += new System.EventHandler(this.Form1_Load);
            this.ResumeLayout(false);

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

        private void Form1_Load(object sender, System.EventArgs e)
        {
            SECURITY_ATTRIBUTES lpSecurityAttributes = new SECURITY_ATTRIBUTES();
            DirectorySecurity security = new DirectorySecurity();
            lpSecurityAttributes.nLength = Marshal.SizeOf(lpSecurityAttributes);
            byte[] src = security.GetSecurityDescriptorBinaryForm();
            IntPtr dest = Marshal.AllocHGlobal(src.Length);
            Marshal.Copy(src, 0, dest, src.Length);
            lpSecurityAttributes.lpSecurityDescriptor = dest;
            string path = @"C:\Test";
            CreateDirectory(path, lpSecurityAttributes);
        }
    }
}
```
