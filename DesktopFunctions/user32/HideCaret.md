
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool HideCaret(IntPtr hWnd);
```

## VB.Net Signature:
```cs
<DllImport("user32")> _
Private Shared Function HideCaret(ByVal hWnd As IntPtr) As Integer
End Function
```

## Sample Code (C#):
```cs
// Hide a textbox control's caret
var textBox = new TextBox();
HideCaret(textBox.Handle);
```

## Sample Code (VB):
```cs
InitializeComponent()
  tb = New TextBox
  Me.Controls.Add(tb)
  showCaret = False
```

## Sample Code (VB):
```cs
If showCaret = False Then HideCaret(tb.Handle)
```
