
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
   [return: MarshalAs(UnmanagedType.Bool)]
   static extern bool PrintWindow(IntPtr hwnd, IntPtr hDC, uint nFlags);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function PrintWindow(ByVal hwnd As IntPtr, ByVal hDC As IntPtr, ByVal nFlags As UInteger) As Boolean
End Function
```

## Sample Code:
```cs
Graphics g = form.CreateGraphics();
Bitmap bmp = new Bitmap(form.Size.Width, form.Size.Height, g);
Graphics memoryGraphics = Graphics.FromImage(bmp);
IntPtr dc = memoryGraphics.GetHdc();
bool success = PrintWindow(form.Handle, dc, 0);
memoryGraphics.ReleaseHdc(dc);
// bmp now contains the screenshot
```

## Sample Code:
```cs
Me.AutoRedraw = True
PrintWindow Me.hWnd, Me.hDC, 0
```

## What if it doesn't work:
```cs
Quote from https://stackoverflow.com/users/7019029/geoff:
I was stuck for ages on this, then found that I can pass a parameter of PW_RENDERFULLCONTENT as the last parameter to PrintWindow.  Googling that shows it's new in Windows 8.1 so presumably doesn't work on 7. It may be worth trying it though, Winuser.h defines it  as
#if(_WIN32_WINNT >= 0x0603)
#define PW_RENDERFULLCONTENT    0x00000002
#endif /* _WIN32_WINNT >= 0x0603 */
```
