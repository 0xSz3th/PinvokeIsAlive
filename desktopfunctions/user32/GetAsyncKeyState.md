<DllImport("user32.dll")> _
    Shared Function GetAsyncKeyState(ByVal vKey As System.Windows.Forms.Keys) As Short
    End Function
// this is import of libraries
    [DllImport("User32.dll")]
    private static extern short GetAsyncKeyState(System.Windows.Forms.Keys vKey); // Keys enumeration

    [DllImport("User32.dll")]
    private static extern short GetAsyncKeyState(System.Int32 vKey);

    string keyBuffer = string.Empty;

    private void timer1_Tick(object sender, EventArgs e)
    {
    timer1.Interval = 3;
    foreach (System.Int32 i in Enum.GetValues(typeof(Keys)))
    {
        int x = GetAsyncKeyState(i);
        if ((x == 1) || (x == Int16.MinValue)) //Use constants (0x8000 and -32768 is Int16.MaxValue)
        {
        keyBuffer += Enum.GetName(typeof(Keys), i) + " ";//this is WinAPI listener of the keys
        }
    }
    if (keyBuffer != "")
    {
        // replacing of unreadable keys          
        keyBuffer = keyBuffer.Replace("Space", "_");
        keyBuffer = keyBuffer.Replace("Delete", "_Del_");
        keyBuffer = keyBuffer.Replace("LShiftKey", "_SHIFT_");
        keyBuffer = keyBuffer.Replace("ShiftKey", "");
        keyBuffer = keyBuffer.Replace("OemQuotes", "!");
        keyBuffer = keyBuffer.Replace("Oemcomma", "?");
        keyBuffer = keyBuffer.Replace("D8", "á");
        keyBuffer = keyBuffer.Replace("D2", "ě");
        keyBuffer = keyBuffer.Replace("D3", "š");
        keyBuffer = keyBuffer.Replace("D4", "č");
        keyBuffer = keyBuffer.Replace("D5", "ř");
        keyBuffer = keyBuffer.Replace("D6", "ž");
        keyBuffer = keyBuffer.Replace("D7", "ý");
        keyBuffer = keyBuffer.Replace("D9", "í");
        keyBuffer = keyBuffer.Replace("D0", "é");
        keyBuffer = keyBuffer.Replace("Back", "<==");
        keyBuffer = keyBuffer.Replace("LButton", "");
        keyBuffer = keyBuffer.Replace("RButton", "");
        keyBuffer = keyBuffer.Replace("NumPad", "");
        keyBuffer = keyBuffer.Replace("OemPeriod", ".");
        keyBuffer = keyBuffer.Replace("OemSemicolon", "ů");
        keyBuffer = keyBuffer.Replace("Oem4", "/");
        keyBuffer = keyBuffer.Replace("LControlKey", "");
        keyBuffer = keyBuffer.Replace("ControlKey", "_CTRL_");
        keyBuffer = keyBuffer.Replace("Enter", "");
        keyBuffer = keyBuffer.Replace("Shift", "____SHIFT___");
        keyBuffer = keyBuffer.ToLower();
        keyBuffer = keyBuffer.Replace(" ", "");
        textBox1.Text = keyBuffer;
    }
    }
[DllImport("user32.dll")]
    static extern ushort GetAsyncKeyState(int vKey);

    public static bool IsKeyPushedDown(System.Windows.Forms.Keys vKey) {
    return 0 != (GetAsyncKeyState((int)vKey) & 0x8000);
    }
<DllImport("user32.dll")> _
     Shared Function GetAsyncKeyState(ByVal vKey As System.Windows.Forms.Keys) As Short
     End Function

     Private Sub Timer1_Tick(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Timer1.Tick
     If GetAsyncKeyState(Keys.Return) <> 0 Then
     TextBox1.Text = "Enter pressed now"
     Else
     TextBox1.Text = "Enter not pressed now"
     End If
     End Sub
