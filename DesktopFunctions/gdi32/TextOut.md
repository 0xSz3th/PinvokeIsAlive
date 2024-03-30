
## C# Signature:
```cs
[DllImport("gdi32.dll", CharSet = CharSet.Auto)]
static extern bool TextOut(IntPtr hdc, int nXStart, int nYStart,
   string lpString, int cbString); (Please see note for CharSet in tips)
```

## VB.NET Signature: 
```cs
<DllImport("gdi32")> _
    Shared Function TextOut(ByVal hdc As IntPtr, ByVal x As Integer, _ 
      ByVal y As Integer, ByVal textstring As String, _
      ByVal charCount As Integer) As Boolean
    End Function
```

## Sample Code:
```cs
// Paste this at the beginning of your file if not present:
   using System.Drawing;
   using System.Runtime.InteropServices;

   //Create a class that subclass Control and paste these methods into it.
   //Then place the new control on a form.

   [DllImport("gdi32.dll")]
   static extern bool TextOut(IntPtr hdc, int nXStart, int nYStart,
       string lpString, int cbString);
   [DllImport("gdi32.dll")]
   static extern bool GetTextExtentPoint(IntPtr hdc, string lpString,
       int cbString, ref Size lpSize);
   [DllImport("gdi32.dll")]
   public static extern IntPtr SelectObject(IntPtr hdc, IntPtr hgdiobj);
   [DllImport("GDI32.dll")]
   public static extern bool DeleteObject(IntPtr objectHandle);

    #region Font

   protected override void OnKeyPress(KeyPressEventArgs e)
   {
       Text += e.KeyChar.ToString();

       //Note, painting should not be done in the OnKeyPress method, instead:
       Refresh();

       //You may want to meassure the string's size for layout purposes.
       using(Graphics g = base.CreateGraphics())
       {

       //Do the GetHdc(), GetTextExtentPoint, etc, here. Remember that you have
       //to delete related objects such as fonts and call ReleaseHdc on graphics 
       //afterwards. If you for some reason don't want to do this you can use a 
       //SafeHandle (needs to be subclassed) which does this for you.

       //Remember to use HandleRef when appropriate. For instance if you create
       //a color that you set through SelectObject the .net garbage collector will
       //happily delete the color unless you refere to it after the drawing call or 
       //use a HandleRef.

       //In this example we used the base class font and therefore need not worry 
       //about the GC deleting the Font in mid drawing.    

       //Also keep in mind that all graphics objects _you_ create must be disposed,
       //which is done through the using clause in this example. It can also be done
       //by calling g.Dispose() in a finally clause (to guarantee that it's executed)
       }
   }

   protected override void OnPaint(PaintEventArgs e)
   {
    IntPtr HDC = e.Graphics.GetHdc();

    //We have to use SelectObject to set the font, color and other properties.
    IntPtr last_font = SelectObject(HDC, Font.ToHfont());

    Size MeasureSize = new Size(0, 0);
    int y_pos = 0;
    int x_pos = 2;

    //Tasks such as these should not be done in the drawing loop as they
    //slow down the drawing.
    String[] lines = Text.Split(new char[] { '\n' });         

    try
    {  
        //We draw out each line of text.
        for(int c=0; c < lines.Length; c++)
        {
             String line = lines[c];
            TextOut(HDC, x_pos, y_pos, line, line.Length);

            //Unless you change the font, the line height never 
            //changes so measuring the text at each draw call is
            //inefficient. Also it measure empty lines at 0 height
            //so pressing multiple enters will not move the text down.
             GetTextExtentPoint(HDC, line, line.Length, ref MeasureSize);

             y_pos += MeasureSize.Height;

            //You can use the MeasureSize.Width property to implement
            //word wrapping.
        }
    }
    finally
    {
        //Put here to make sure we don't get a memory leak.

        DeleteObject(SelectObject(HDC, last_font));
        e.Graphics.ReleaseHdc(HDC);
        //Don't call dispose() on the Graphics object unless you createded it.
    }
   }
```

##  Vb.net Sample:
```cs
Declare Function SetTextCharacterExtra Lib "gdi32" Alias "SetTextCharacterExtra" (ByVal hDC As Integer, ByVal nCharExtra As Integer) As Integer
    <DllImport("gdi32")> _
    Private Shared Function TextOut(ByVal hdc As IntPtr, ByVal x As Integer, ByVal y As Integer, ByVal textstring As String, ByVal charCount As Integer) As Boolean
    End Function
    <DllImport("gdi32")> _
    Private Shared Function SelectObject(ByVal hdc As IntPtr, ByVal hgdiobj As IntPtr) As IntPtr
    End Function
    <DllImport("gdi32")> _
    Private Shared Function DeleteObject(ByVal objectHandle As IntPtr) As Boolean
    End Function
    <DllImport("gdi32")> _
    Private Shared Function SetBkColor(ByVal hdc As IntPtr, ByVal crColor As Integer) As UInt32
    End Function
    <DllImport("gdi32")> _
    Private Shared Function SetTextColor(ByVal hdc As IntPtr, ByVal crColor As Integer) As UInt32
    End Function

    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click
    Using G = Graphics.FromHwnd(Me.Handle)
        Using myFont As New System.Drawing.Font("Arial", 20, FontStyle.Regular, GraphicsUnit.Pixel)
        'Regular Way
        Dim LeftEdge = 20
        G.DrawString("Hello", myFont, Brushes.Red, LeftEdge, 40)

        'If you want kerning
        Dim Kerning As Integer = 6 'I think this is twips
        Dim Hdc As IntPtr
        Dim FontPtr As IntPtr
        Try
            'Grab the Graphic object's handle
            Hdc = G.GetHdc()
            'Set the current GDI font
            FontPtr = SelectObject(Hdc, myFont.ToHfont())
            'Set the drawing surface background color
            SetBkColor(Hdc, ColorTranslator.ToWin32(Me.BackColor))
            'Set the text color
            SetTextColor(Hdc, ColorTranslator.ToWin32(Color.Red))
            'Set the kerning
            SetTextCharacterExtra(Hdc, Kerning)
            Dim Text = "Hello"
            'Draw the text at (20,60), Kerning will be applied so reset the left edge to half of kerning
            TextOut(Hdc, LeftEdge + (Kerning \ 2), 60, Text, Text.Length)
        Catch ex As Exception

        Finally
            'Release the font
            DeleteObject(FontPtr)
            'Release the handle on the graphics object
            G.ReleaseHdc()
        End Try
        End Using
    End Using
    End Sub
```

## Alternative Managed API:
```cs
Graphics.DrawString
Graphics.MeasureString
Graphics.MeasureCharacterRanges
```
