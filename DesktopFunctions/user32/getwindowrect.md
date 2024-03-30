
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern bool GetWindowRect(IntPtr hwnd, out RECT lpRect);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function GetWindowRect(ByVal hWnd As HandleRef, ByRef lpRect As RECT) As Boolean
End Function
```

## Sample Code:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool GetWindowRect(HandleRef hWnd, out RECT lpRect);

[StructLayout(LayoutKind.Sequential)]
public struct RECT
{
     public int Left;        // x position of upper-left corner
     public int Top;         // y position of upper-left corner
     public int Right;       // x position of lower-right corner
     public int Bottom;      // y position of lower-right corner
}

Rectangle myRect = new Rectangle();

private void button1_Click(object sender, System.EventArgs e)
{
     RECT rct;

     if(!GetWindowRect(new HandleRef(this, this.Handle), out rct ))
     {
     MessageBox.Show("ERROR");
             return;
     }
     MessageBox.Show( rct.ToString() );

     myRect.X = rct.Left;
     myRect.Y = rct.Top;
     myRect.Width = rct.Right - rct.Left + 1;
     myRect.Height = rct.Bottom - rct.Top + 1;
}
```
