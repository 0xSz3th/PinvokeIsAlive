
## C# Signature:
```cs
[DllImport("user32.dll")]
public static extern bool SetLayeredWindowAttributes(IntPtr hwnd, uint crKey, byte bAlpha, uint dwFlags);
```

## VB Signature:
```cs
Public Declare Auto Function SetLayeredWindowAttributes Lib "User32.Dll" _
    (ByVal hWnd As IntPtr, ByVal crKey As Integer, ByVal Alpha As Byte, ByVal dwFlags As Integer) As Boolean
```

## User-Defined Types:
```cs
[Flags]
public enum LayeredWindowFlags
{
     LWA_ALPHA = 0x00000002,
     LWA_COLORKEY = 0x00000001,
}
```

## C# Sample Code:
```cs
public const int GWL_EXSTYLE = -20;
    public const int WS_EX_LAYERED = 0x80000;
    public const int LWA_ALPHA = 0x2;
    public const int LWA_COLORKEY = 0x1;

    //set the window style to alpha appearance
    private void button4_Click(object sender, EventArgs e)
    {
        SetWindowLong(Handle, GWL_EXSTYLE, GetWindowLong(Handle, GWL_EXSTYLE) ^ WS_EX_LAYERED);
        SetLayeredWindowAttributes(Handle, 0, 128, LWA_ALPHA);
    }
```
