
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool DrawAnimatedRects(IntPtr hwnd, int idAni,
   [In] ref RECT lprcFrom, [In] ref RECT lprcTo);
```

## Sample Code:
```cs
/// <summary>
    /// This constant is not implemented on any Windows platform!
    /// </summary>
    public const System.Int32 IDANI_OPEN = 1;

    /// <summary>
    /// The window caption will animate from lprcFrom to lprcTo.
    /// </summary>
    public const System.Int32 IDANI_CAPTION = 3;

    [System.Runtime.InteropServices.StructLayout(System.Runtime.InteropServices.LayoutKind.Sequential)]
    struct RECT 
    {
      public RECT(System.Drawing.Rectangle rectangle) 
      {
        Left = rectangle.Left;
        Top = rectangle.Top;
        Right = rectangle.Right;
        Bottom = rectangle.Bottom;
      }
      public RECT(System.Drawing.Point location, System.Drawing.Size size) 
      {
        Left = location.X;
        Top = location.Y;
        Right = location.X + size.Width;
        Bottom = location.Y + size.Height;
      }
      public System.Int32 Left;
      public System.Int32 Top;
      public System.Int32 Right;
      public System.Int32 Bottom;
    }

    [System.Runtime.InteropServices.DllImport("user32.dll")]
    static extern bool DrawAnimatedRects(System.IntPtr hwnd, int idAni,
      [System.Runtime.InteropServices.In] ref RECT lprcFrom, 
      [System.Runtime.InteropServices.In] ref RECT lprcTo);

    [System.Runtime.InteropServices.DllImport("user32.dll", SetLastError = true)]
    static extern System.IntPtr FindWindow(string lpClassName, string lpWindowName);

    [System.Runtime.InteropServices.DllImport("user32.dll", SetLastError = true)]
    static extern System.IntPtr FindWindowEx(System.IntPtr hwndParent, System.IntPtr hwndChildAfter,
      string lpszClass, string lpszWindow);

    [System.Runtime.InteropServices.DllImport("user32.dll")]
    static extern bool GetWindowRect(System.IntPtr hWnd, out RECT lpRect);

    /// <summary>
    /// Show or hide a form with animation.
    /// </summary>
    /// <param name="form">The form reference to be animated.</param>
    /// <param name="show">If true the form will be animated as if opening, otherwise as if closing.</param>
    static public void ShowHideAnimated(System.Windows.Forms.Form form, System.Boolean show) 
    {
      RECT from = new RECT(form.Location, form.Size);
      RECT to;

      System.IntPtr hWnd = 
        FindWindowEx(FindWindow("Shell_TrayWnd", null), System.IntPtr.Zero, "TrayNotifyWnd", null);

      if (hWnd != System.IntPtr.Zero) 
      {
        GetWindowRect(hWnd, out to);
      }
      else
      {
        to.Left = System.Windows.Forms.SystemInformation.VirtualScreen.Right - form.Width;
        to.Top = System.Windows.Forms.SystemInformation.VirtualScreen.Bottom -
          System.Windows.Forms.SystemInformation.CaptionHeight -
            (System.Windows.Forms.SystemInformation.FrameBorderSize.Height * 2);
        to.Right = System.Windows.Forms.SystemInformation.VirtualScreen.Right;
        to.Bottom = System.Windows.Forms.SystemInformation.VirtualScreen.Bottom;
      }

      if (show) 
      {
        DrawAnimatedRects(form.Handle, IDANI_CAPTION, ref to, ref from);
        form.Show();
      }
      else 
      {
        form.Hide();
        DrawAnimatedRects(form.Handle, IDANI_CAPTION, ref from, ref to);
      }
    }
```

## Alternative Managed API:
```cs
[StructLayout(System::Runtime::InteropServices::LayoutKind::Sequential)]
    ref struct RECT {
    public:
    RECT() {
    }

    RECT(System::Drawing::Rectangle rectangle) {
        Left = rectangle.Left;
        Top = rectangle.Top;
        Right = rectangle.Right;
        Bottom = rectangle.Bottom;
    }

    RECT(System::Drawing::Point location, System::Drawing::Size size) {
        Left = location.X;
        Top = location.Y;
        Right = location.X + size.Width;
        Bottom = location.Y + size.Height;
    }

    System::Int32 Left;
    System::Int32 Top;
    System::Int32 Right;
    System::Int32 Bottom;
    };

    [DllImport("user32.dll")]
    bool DrawAnimatedRects(int hwnd, int idAni, RECT^ lprcFrom, RECT^ lprcTo);

    [DllImport("user32.dll", SetLastError = true)]
    int FindWindow(String^ lpClassName, String^ lpWindowName);

    [DllImport("user32.dll", SetLastError = true)]
    int FindWindowEx(int hwndParent, int hwndChildAfter,
      String^ lpszClass, String^ lpszWindow);

    [DllImport("user32.dll")]
    bool GetWindowRect(int hWnd, RECT^ lpRect);

    static const int IDANI_OPEN = 1;
    static const int IDANI_CAPTION = 3;

    void ShowHideAnimated(bool show) {
    RECT^ from=gcnew RECT(this->Location, this->Size);
    RECT^ to=gcnew RECT();

    int hWnd=FindWindowEx(FindWindow("Shell_TrayWnd", nullptr), 0, "TrayNotifyWnd", nullptr);

    if (hWnd != 0) {
        GetWindowRect(hWnd, to);
    }
    else {
          to->Left = System::Windows::Forms::SystemInformation::VirtualScreen.Rig ht - 32;
          to->Top = System::Windows::Forms::SystemInformation::VirtualScreen.Bot tom -32;
          to->Right = System::Windows::Forms::SystemInformation::VirtualScreen.Rig ht;
          to->Bottom = System::Windows::Forms::SystemInformation::VirtualScreen.Bot tom;
    }

    if (show) {
        DrawAnimatedRects(this->Handle.ToInt32(), IDANI_CAPTION, to, from);
        this->Show();
    }
    else {
        this->Hide();
        DrawAnimatedRects(this->Handle.ToInt32(), IDANI_CAPTION, from, to);
    }
    }
```
