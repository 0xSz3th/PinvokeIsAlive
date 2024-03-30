
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreateDC(string lpszDriver, string lpszDevice,
   string lpszOutput, IntPtr lpInitData);
```

## VB.NET Signature
```cs
<DllImport("gdi32.dll", SetLastError:=True, CharSet:=CharSet.Ansi)> _
public Function CreateDC(<MarshalAs(UnmanagedType.LPStr)>lpszDriver As String, _
              <MarshalAs(UnmanagedType.LPStr)>lpszDevice As String, _
              <MarshalAs(UnmanagedType.LPStr)>lpszOutput As String, _
              lpInitData As IntPtr) As IntPtr
End Function
```

## VB Signature:
```cs
Declare Function CreateDC Lib "gdi32.dll" ( _
   lpszDriver As String, lpszDevice As String, _
   lpszOutput As String, lpInitData As IntPtr) As IntPtr
```

## Sample Code:
```cs
public partial class Form1 : Form
    {
    public Form1()
    {
        InitializeComponent(); 
        hdc = CreateDC("DISPLAY", null, null, IntPtr.Zero); // create a new dc,yeni bir dc yaratıyoruz.Yeni bir system dc si yaratıyoruz.
    }
    [DllImport("gdi32.dll", EntryPoint = "CreateDC", CharSet = CharSet.Auto, SetLastError = true)]
    private static extern IntPtr CreateDC(string lpszDriver, string lpszDeviceName, string lpszOutput, IntPtr devMode);

    [DllImport("gdi32.dll")]
    static extern uint SetPixel(IntPtr hdc, int X, int Y, uint crColor); // Bu fonksiyon verdiğimiz dc ye sahip grafiklere piksel girer.
    IntPtr hdc; 

    private void timer1_Tick(object sender, EventArgs e)
    {
        for (int x = 0; x < 1000; x += 5)
        {
        for (int y = 0; y < 1000; y += 5)
        {
            SetPixel(hdc, x, y, (uint)Color.Black.ToArgb());
        }
        }
    }
    }
```
