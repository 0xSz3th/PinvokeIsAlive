
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool SwapMouseButton(bool fSwap);
```

## Sample Code - C# = sivakumar.keerthi
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
        static extern bool SwapMouseButton(bool fSwap);
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
            this.ClientSize = new System.Drawing.Size(292, 266);
            this.Name = "Form1";
            this.Text = "Form1";
            this.Load += new System.EventHandler(this.Form1_Load);

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
            //fSwap
            // true - swaps mouse button( right click will do left click functions and left click will do right click functions )
            // false - undo the process of swap.
            SwapMouseButton( true );
        }
    }
```

## Another sample:
```cs
public partial class Form1 : Form
    {
    public Form1()
    {
        InitializeComponent();
    }
    [DllImport("user32.dll")]
    static extern long SwapMouseButton(long bSwap);

    private void button1_Click(object sender, EventArgs e)
    {
        SwapMouseButton(1);
    }

    private void button2_Click(object sender, EventArgs e)
    {
        SwapMouseButton(0);
    }
    }
```
