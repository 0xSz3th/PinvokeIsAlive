
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern void mouse_event(uint dwFlags, int dx, int dy, uint dwData,
   UIntPtr dwExtraInfo);
```

## C# Signature:
```cs
[DllImport("user32.dll")]
static extern void mouse_event(uint dwFlags, int dx, int dy, uint dwData,
  int dwExtraInfo);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Sub mouse_event(dwFlags As UInteger, dx As UInteger, dy As UInteger, dwData As UInteger, dwExtraInfo As Integer)
End Sub
```

## VB Signature
```cs
Public Declare Sub mouse_event Lib "user32" (ByVal dwFlags As Long, ByVal dx As Long, ByVal dy As Long, ByVal dwData As Long, ByVal dwExtraInfo As Long)
```

## User-Defined Constants:
```cs
const uint MOUSEEVENTF_ABSOLUTE = 0x8000;
const uint MOUSEEVENTF_LEFTDOWN = 0x0002;
const uint MOUSEEVENTF_LEFTUP = 0x0004;
const uint MOUSEEVENTF_MIDDLEDOWN = 0x0020;
const uint MOUSEEVENTF_MIDDLEUP = 0x0040;
const uint MOUSEEVENTF_MOVE = 0x0001;
const uint MOUSEEVENTF_RIGHTDOWN = 0x0008;
const uint MOUSEEVENTF_RIGHTUP = 0x0010;
const uint MOUSEEVENTF_XDOWN = 0x0080;
const uint MOUSEEVENTF_XUP = 0x0100;
const uint MOUSEEVENTF_WHEEL = 0x0800;
const uint MOUSEEVENTF_HWHEEL = 0x01000;
```

## User-Defined Constants:
```cs
<Flags()> _
Public Enum MouseEventFlags As UInteger
     MOUSEEVENTF_ABSOLUTE = &H8000
     MOUSEEVENTF_LEFTDOWN = &H2
     MOUSEEVENTF_LEFTUP = &H4
     MOUSEEVENTF_MIDDLEDOWN = &H20
     MOUSEEVENTF_MIDDLEUP = &H40
     MOUSEEVENTF_MOVE = &H1
     MOUSEEVENTF_RIGHTDOWN = &H8
     MOUSEEVENTF_RIGHTUP = &H10
     MOUSEEVENTF_XDOWN = &H80
     MOUSEEVENTF_XUP = &H100
     MOUSEEVENTF_WHEEL = &H800
     MOUSEEVENTF_HWHEEL = &H1000
End Enum
```

## User-Defined Types:
```cs
[Flags]
  public enum MouseEventFlags : uint
  {
    LEFTDOWN   = 0x00000002,
    LEFTUP     = 0x00000004,
    MIDDLEDOWN = 0x00000020,
    MIDDLEUP   = 0x00000040,
    MOVE       = 0x00000001,
    ABSOLUTE   = 0x00008000,
    RIGHTDOWN  = 0x00000008,
    RIGHTUP    = 0x00000010,
    WHEEL      = 0x00000800,
    XDOWN      = 0x00000080,
    XUP    = 0x00000100
  }

  //Use the values of this enum for the 'dwData' parameter
  //to specify an X button when using MouseEventFlags.XDOWN or
  //MouseEventFlags.XUP for the dwFlags parameter.
  public enum MouseEventDataXButtons : uint
  {
    XBUTTON1   = 0x00000001,
    XBUTTON2   = 0x00000002
  }
```

## VB.Net Signature:
```cs
Declare Function apimouse_event Lib "user32.dll" Alias "mouse_event" (ByVal dwFlags As Int32, ByVal dX As Int32, ByVal dY As Int32, ByVal cButtons As Int32, ByVal dwExtraInfo As Int32) As Boolean
```

## C# Sample Code 1:
```cs
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Text;
using System.Windows.Forms;

using System.Runtime.InteropServices;
using System.Threading;

namespace PInvoke_DllImport_Cs
{
     public partial class Form1 : Form
     {
     public Form1()
     {
         InitializeComponent();
     }

     const uint MOUSEEVENTF_LEFTDOWN = 0x0002;
     const uint MOUSEEVENTF_LEFTUP = 0x0004;

     [DllImport("user32.dll")]
     private static extern void mouse_event(uint dwFlags, uint dx, uint dy, uint dwData, int dwExtraInfo);

     private void timer1_Tick(System.Object sender, System.EventArgs e)
     {
         mouse_event(MOUSEEVENTF_LEFTDOWN, 0, 0, 0, 0);
         Thread.Sleep(100);
         mouse_event(MOUSEEVENTF_LEFTUP, 0, 0, 0, 0);
     }
     }
}
```

## C# Sample Code 2:
```cs
[DllImport("user32.dll")]
    static extern void mouse_event(int dwFlags, int dx, int dy, int dwData, int dwExtraInfo);

    [Flags]
    public enum MouseEventFlags
    {
        LEFTDOWN = 0x00000002,
        LEFTUP = 0x00000004,
        MIDDLEDOWN = 0x00000020,
        MIDDLEUP = 0x00000040,
        MOVE = 0x00000001,
        ABSOLUTE = 0x00008000,
        RIGHTDOWN = 0x00000008,
        RIGHTUP = 0x00000010
    }

    public static void LeftClick(int x, int y)
    {
        Cursor.Position = new System.Drawing.Point(x, y);
        mouse_event((int)(MouseEventFlags.LEFTDOWN), 0, 0, 0, 0);
        mouse_event((int)(MouseEventFlags.LEFTUP), 0, 0, 0, 0);
    }
```

## VB.NET Sample Code 1:
```cs
' Clicks left mouse button in current coordinates

Imports System.Runtime.InteropServices
Imports System.Threading

Public Class Form1

     Const MOUSEEVENTF_LEFTDOWN As UInteger = &H2 '0x0002
     Const MOUSEEVENTF_LEFTUP As UInteger = &H4 '0x0004

     <DllImport("user32.dll")> _
     Private Shared Sub mouse_event(ByVal dwFlags As UInteger, ByVal dx As UInteger, ByVal dy As UInteger, ByVal dwData As UInteger, ByVal dwExtraInfo As Integer)
     End Sub

     'Public Declare Sub mouse_event Lib "user32" (ByVal dwFlags As Long, ByVal dx As Long, ByVal dy As Long, ByVal dwData As Long, ByVal dwExtraInfo As Long)

     Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick
     mouse_event(MOUSEEVENTF_LEFTDOWN, 0, 0, 0, 0)
     Thread.Sleep(100)
     mouse_event(MOUSEEVENTF_LEFTUP, 0, 0, 0, 0)
     End Sub

End Class
```

## VB.NET Sample Code 2:
```cs
Const MOUSEEVENTF_WHEEL As Int32 = 2048
    Const MOUSEEVENTF_WHEEL_DELTA As Int32 = 120

    Private Declare Function apimouse_event Lib "user32" Alias "mouse_event" (ByVal dwFlags As Int32, ByVal dX As Int32, ByVal dY As Int32, ByVal cButtons As Int32, ByVal dwExtraInfo As Int32) As Boolean
    Private Declare Function apiGetMessageExtraInfo Lib "user32" Alias "GetMessageExtraInfo" () As Int32

    Private Sub PlayScroll(ByVal number As Int32, Optional ByVal increment As Int32 = 2)
    On Error Resume Next
    For i As Int32 = 1 To number
        apimouse_event(MOUSEEVENTF_WHEEL, 0, 0, increment, apiGetMessageExtraInfo)
    Next
    End Sub
```

## VB.NET 2005 Sample Code:
```cs
Inherits System.Windows.Forms.Form

    Declare Auto Sub mouse_event Lib "user32" (ByVal dwFlags As Int32, ByVal dx As Int32, ByVal dy As Int32, ByVal cButtons As Int32, ByVal dwExtraInfo As IntPtr)

    Const MOUSEEVENTF_MOVE As Int32 = &H1 '  mouse move
    Const MOUSEEVENTF_LEFTDOWN As Int32 = &H2 '  left button down
    Const MOUSEEVENTF_LEFTUP As Int32 = &H4 '  left button up
    Const MOUSEEVENTF_RIGHTDOWN As Int32 = &H8 '  right button down
    Const MOUSEEVENTF_RIGHTUP As Int32 = &H10 '  right button up
    Const MOUSEEVENTF_MIDDLEDOWN As Int32 = &H20 '  middle button down
    Const MOUSEEVENTF_MIDDLEUP As Int32 = &H40 '  middle button up
    Const MOUSEEVENTF_ABSOLUTE As Int32 = &H8000 '  absolute move
    Const MOUSEEVENTF_WHEEL As Int32 = &H800 ' wheel button rolled

    ' Simulate moving the mouse to the center of the
    ' PictureBox and clicking.
    Private Sub cmdClick_Click(ByVal eventSender As System.Object, ByVal eventArgs As System.EventArgs) Handles cmdClick.Click
    Dim cur_x As Single
    Dim cur_y As Single
    Dim dest_x As Single
    Dim dest_y As Single

    ' mouse_event moves in a coordinate system where
    ' (0, 0) is in the upper left corner and
    ' (65535,65535) is in the lower right corner.

    ' Get the current mouse coordinates and convert
    ' them into this new system.
    cur_x = System.Windows.Forms.Cursor.Position.X * 65535 / System.Windows.Forms.Screen.PrimaryScreen.Bounds.Width
    cur_y = System.Windows.Forms.Cursor.Position.Y * 65535 / System.Windows.Forms.Screen.PrimaryScreen.Bounds.Height

    ' Convert the coordinates of the center of the
    ' picClicker PictureBox into this new system.
    Dim pt As Point = picClicker.PointToScreen(New Point(picClicker.ClientRectangle.Width / 2, picClicker.ClientRectangle.Height / 2))

    dest_x = pt.X * 65535 / System.Windows.Forms.Screen.PrimaryScreen.Bounds.Width
    dest_y = pt.Y * 65535 / System.Windows.Forms.Screen.PrimaryScreen.Bounds.Height

    txtResults.Text = txtResults.Text & "From " & System.Windows.Forms.Cursor.Position.X & " " & System.Windows.Forms.Cursor.Position.Y & " to " & pt.X & " " & pt.Y & vbCrLf
    txtResults.Text = txtResults.Text & "From " & cur_x & " " & cur_y & " to " & dest_x & " " & dest_y & vbCrLf

    ' Move the mouse to its final destination and click it.
    mouse_event(MOUSEEVENTF_ABSOLUTE + MOUSEEVENTF_MOVE + MOUSEEVENTF_LEFTDOWN + MOUSEEVENTF_LEFTUP, dest_x, dest_y, 0, 0)
    End Sub

    Private Sub picClicker_Click(ByVal eventSender As System.Object, ByVal eventArgs As System.EventArgs) Handles picClicker.Click
    txtResults.Text = txtResults.Text & "MouseClick" & vbCrLf
    End Sub

    Private Sub picClicker_MouseDown(ByVal sender As System.Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles picClicker.MouseDown
    txtResults.Text = txtResults.Text & "MouseDown (" & e.X & ", " & e.Y & ")" & vbCrLf
    End Sub

    Private Sub picClicker_MouseUp(ByVal sender As System.Object, ByVal e As System.Windows.Forms.MouseEventArgs) Handles picClicker.MouseUp
    txtResults.Text = txtResults.Text & "MouseUp (" & e.X & ", " & e.Y & ")" & vbCrLf
    End Sub
```
