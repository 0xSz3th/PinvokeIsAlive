
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
  [return: MarshalAs(UnmanagedType.Bool)]
  static extern bool RemoveClipboardFormatListener(IntPtr hwnd);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=true)> _
  Public Shared Function RemoveClipboardFormatListener(hWnd As IntPtr) As <MarshalAs(UnmanagedType.Bool)>Boolean
```

## Sample Code:
```cs
// C# Example:
// Declare the API method for placing the given window in the system-maintained clipboard format listener list.
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool AddClipboardFormatListener(IntPtr hwnd);

// Declare the API method for removing the given window from the system-maintained clipboard format listener list.
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool RemoveClipboardFormatListener(IntPtr hwnd);

// Here is the message sent when the contents of the clipboard have changed.
private const int WM_CLIPBOARDUPDATE = 0x031D;

// Here is how to add our window to the Clipboard Format Listener:
AddClipboardFormatListener(this.Handle);

// Here is how to process The Message:    
protected override void WndProc(ref Message m)
{
    base.WndProc(ref m);

    if (m.Msg == WM_CLIPBOARDUPDATE)
    {
        IDataObject iData = Clipboard.GetDataObject();      // Clipboard's data.

        if (iData.GetDataPresent(DataFormats.Text))
        {
            string text = (string)iData.GetData(DataFormats.Text);
            // do something with it
        }
        else if (iData.GetDataPresent(DataFormats.Bitmap))
        {
            Bitmap image = (Bitmap)iData.GetData(DataFormats.Bitmap);
            // do something with it
        }
        // you can also check for more formats and process accordingly
    }
}

// When closing your program, first remove the format listener:
private void Form1_FormClosing(object sender, FormClosingEventArgs e)
{
    RemoveClipboardFormatListener(this.Handle);     // Remove our window from the clipboard's format listener list.
}
```
