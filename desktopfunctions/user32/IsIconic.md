
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool IsIconic(IntPtr hWnd);
```

## VB Signature:
```cs
Private Declare Auto Function IsIconic Lib "user32.dll" (ByVal hwnd As IntPtr) As Boolean
```

## Sample Code - C# - sivakumar.keerthi
```cs
/// <summary>
    /// Summary description for Form1.
    /// </summary>
    public class Form1 : System.Windows.Forms.Form
    {
        /// <summary>
        /// Required designer variable.
        /// </summary>
        [DllImport("user32.dll")]
        public static extern IntPtr FindWindow( string sClsName , string sWndName );
        [DllImport("user32.dll")]
        public static extern int SetForegroundWindow( IntPtr Hwnd );
        [DllImport("user32.dll")]
        public static extern int ShowWindow( IntPtr Hwnd , int iCmdShow );
        [DllImport("user32.dll")]
        public static extern bool IsIconic( IntPtr Hwnd );    

        private const int iRestore = 9;
        private const int iShow = 5;

        private System.ComponentModel.Container components = null;

        public Form1()
        {
            //
            // Required for Windows Form Designer support
            //
            InitializeComponent();
            //
            // TODO: Add any constructor code after InitializeComponent call
            //
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
            // 
            // Form1
            // 
            this.AutoScaleBaseSize = new System.Drawing.Size(5, 13);
            this.ClientSize = new System.Drawing.Size(528, 266);
            this.Name = "Form1";
            this.Text = "Form1";
            this.ResumeLayout(false);

        }
        #endregion

        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main() 
        {
            Process[] p = Process.GetProcessesByName( Process.GetCurrentProcess().ProcessName , Environment.MachineName );
            if ( p.Length > 1 )
            {
                MessageBox.Show( "Already one instance is running......." );
                Form1 Frm = new Form1();
                Frm.ShowForm();
                return;
            }
            else
                Application.Run(new Form1());
        }

        private void ShowForm()
        {
            IntPtr Hwnd = FindWindow( null , "Form1" );
            if ( Hwnd.ToInt32() > 0 )
            {
                SetForegroundWindow( Hwnd );
                if ( IsIconic( Hwnd ) )
                    ShowWindow( Hwnd , iRestore );
                else
                    ShowWindow( Hwnd , iShow );
            }
        }
    }
```

## Sample Code:
```cs
// Want only one instance of an application?

      [DllImport("User32.Dll")]
      private static extern bool SetForegroundWindow(IntPtr hWnd);
      [DllImport("User32.Dll")]
      private static extern bool ShowWindowAsync(IntPtr hWnd, int nCmdShow);
      [DllImport("User32.Dll")]
      private static extern bool IsIconic(IntPtr hWnd);


      private const int SW_RESTORE = 9;

      /// <summary>
      /// Main entry point for the application.
      /// </summary>
      [STAThread]
      static int
      Main
    (
      string[] arguments
    ) 
    {
      // Check for running instance

      Process thisProcess = Process.GetCurrentProcess();
      Process[] processes = Process.GetProcessesByName(thisProcess.ProcessName);

      if (processes.Length > 1)
        {
          // One is us (which will end); the other we activate

          int index = 0;
          if (processes[index].Id == thisProcess.Id)
        index = 1;

          IntPtr hWnd = processes[index].MainWindowHandle;

          if (IsIconic(hWnd))
        ShowWindowAsync(hWnd, SW_RESTORE);

          SetForegroundWindow(hWnd);

          // Exit
          return 0;
        }


       // Normal startup code continues here... 

     }
```
