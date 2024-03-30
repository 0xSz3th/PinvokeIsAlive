
## C# Signature:
```cs
/// <summary>
    /// Function to retrieve raw input data.
    /// </summary>
    /// <param name="hRawInput">Handle to the raw input.</param>
    /// <param name="uiCommand">Command to issue when retrieving data.</param>
    /// <param name="pData">Raw input data.</param>
    /// <param name="pcbSize">Number of bytes in the array.</param>
    /// <param name="cbSizeHeader">Size of the header.</param>
    /// <returns>0 if successful if pData is null, otherwise number of bytes if pData is not null.</returns>
    [DllImport("user32.dll")]
    public static extern int GetRawInputData(IntPtr hRawInput, RawInputCommand uiCommand, out RAWINPUT pData, ref int pcbSize, int cbSizeHeader);
```

## C# Signature:
```cs
/// <summary>
    /// Function to retrieve raw input data.
    /// </summary>
    /// <param name="hRawInput">Handle to the raw input.</param>
    /// <param name="uiCommand">Command to issue when retrieving data.</param>
    /// <param name="pData">Raw input data.</param>
    /// <param name="pcbSize">Number of bytes in the array.</param>
    /// <param name="cbSizeHeader">Size of the header.</param>
    /// <returns>0 if successful if pData is null, otherwise number of bytes if pData is not null.</returns>
    [DllImport("user32.dll")]
    public static extern int GetRawInputData(IntPtr hRawInput, RawInputCommand uiCommand, byte[] pData, ref int pcbSize, int cbSizeHeader);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto, EntryPoint:="GetRawInputData", SetLastError:=True)>
    Function GetRawInputData(hRawInput As IntPtr,
                    uiCommand As UInteger,
                    ByRef pData As IntPtr,
                    ByRef pcbSize As IntPtr,
                    cbSizeHeader As UInteger)
    End Function
```

## Sample Code:
```cs
protected override void WndProc(ref Message m)
    {
        if (m.Msg == (int)WindowMessages.RawInput)  // WindowMessages.RawInput = 0x00FF (WM_INPUT)
        {
            RAWINPUT input = new RAWINPUT();
            int outSize = 0;
            int size = Marshal.SizeOf(typeof(RAWINPUT));

            outSize = Win32API.GetRawInputData(m.LParam, RawInputCommand.Input, out input, ref size, Marshal.SizeOf(typeof(RAWINPUTHEADER)));
            if (outSize != -1)
            {
                if (input.Header.Type == RawInputType.Mouse)
                {
                    p.X += input.Mouse.LastX;
                    p.Y += input.Mouse.LastY;
                    label1.Text = "Mouse: " + p.X.ToString() + "x" + p.Y.ToString() + " " + input.Mouse.ButtonFlags.ToString();
                }
            }
        }
        base.WndProc(ref m);
    }
```
