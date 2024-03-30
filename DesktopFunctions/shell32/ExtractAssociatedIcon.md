
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern IntPtr ExtractAssociatedIcon(IntPtr hInst, StringBuilder lpIconPath,
   out ushort lpiIcon);
```

## VB Signature:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Auto)> _
Shared Function ExtractAssociatedIcon _
     (ByVal hInst As IntPtr, _
      ByVal iconPath As StringBuilder, _
      ByRef index As Short) As IntPtr
End Function
```

## Notes:
```cs
If the icon is extracted from an associated executable file, the function stores the full path and file name of the executable file in the string pointed to by lpIconPath, and stores the icon's identifier in the WORD pointed to by lpiIcon.
```

## Sample Code:
```cs
public partial class IconTest : Form
    {
    [DllImport("shell32.dll")]
    static extern IntPtr ExtractAssociatedIcon(IntPtr hInst, StringBuilder lpIconPath,
       out ushort lpiIcon);

    [DllImport("shell32.dll")]
    static extern IntPtr ExtractIcon(IntPtr hInst, string lpszExeFileName, int nIconIndex);

    public IconTest()
    {
        InitializeComponent();
    }

    private void btnBrowse_Click(object sender, EventArgs e)
    {
        openFileDialog1.ShowDialog();

        ushort uicon;
        StringBuilder strB = new StringBuilder(openFileDialog1.FileName);
        IntPtr handle = ExtractAssociatedIcon(this.Handle, strB, out uicon);
        Icon ico = Icon.FromHandle(handle);

        pictureBox1.Image = ico.ToBitmap();
    }
    }
```
