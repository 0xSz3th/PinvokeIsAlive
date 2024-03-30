
## C# Signature:
```cs
[DllImport("winmm.dll")]
static extern Int32 mciSendString(string command, StringBuilder buffer, int bufferSize, IntPtr hwndCallback);
```

## VB.NET Signature:
```cs
<DllImport("winmm.dll")> _
Private Shared Function mciSendString(ByVal command As String, ByVal buffer As StringBuilder, ByVal bufferSize As Integer, ByVal hwndCallback As IntPtr) As Integer
End Function
```

## VB Signature:
```cs
Declare Ansi Function mciSendString Lib "winmm.dll" Alias "mciSendStringA" (ByVal command As String, ByRef buffer As StringBuilder, ByVal bufferSize As Integer, ByVal hWndCallback As IntPtr) As Integer
```

## Sample Code
```cs
// Open CD-ROM Drive Door
public void OpenCD()
{
    IntPtr ptr = IntPtr.Zero;
    StringBuilder returnstring = new StringBuilder();
    mciSendString("set CDAudio door open", returnstring,127, IntPtr.Zero);
}
```

## Sample Code
```cs
// Open Media File
string sCommand = "open \"" + strFilePath + "\" type mpegvideo alias MediaFile";
mciSendString(sCommand, null, 0, 0);

// Play the Media File
sCommand = "play MediaFile notify";
// _frmObject is your form that will handle the notification messages
mciSendString(sCommand, null, 0, _frmObject.Handle.ToInt64());

// Declare the notify constant
public const int MM_MCINOTIFY = 953;

// Override the WndProc function in the form
protected override void WndProc(ref Message m) 
{
    if (m.Msg == MM_MCINOTIFY)
    {
        // The file is done playing, do whatever
    }

    base.WndProc(ref m);
}
```

## Sample Code
```cs
[DllImport("winmm.dll")]
static extern Int32 mciSendString(string command, string buffer, int bufferSize, IntPtr hwndCallback);

private void EjectCdCommand()
{
     string rt = "";
     mciSendString("set CDAudio door open", rt, 127, IntPtr.Zero);
}

private void CloseCdCommand()
{
     string rt = "";
     mciSendString("set CDAudio door closed", rt, 127, IntPtr.Zero);
}
```

## Sample Code
```cs
' Open CD-ROM Drive Door
Public Sub OpenCDDoor()
     Dim returnstring As StringBuilder = New StringBuilder()
     mciSendString("set CDAudio door open", returnstring, 127, IntPtr.Zero)
     MsgBox(returnstring)
End Sub
```

## Sample Code
```cs
' Declare the notify constant
Public Const MM_MCINOTIFY As Integer = 953

' Open and play a media file
Public Sub OpenMediaFile(ByVal strFilePath As String)
     ' Open the media file
     Dim sCommand As String = "open """ + strFilePath + """ type waveaudio alias MediaFile"
     mciSendString(sCommand, Nothing, 0, IntPtr.Zero)

     ' It's is assumed this function is in a Form so Me points to the current instance of the form
     sCommand = "play MediaFile notify"
     mciSendString(sCommand, Nothing, 0, Me.Handle.ToInt64())
End Sub

' Override the WndProc function which is called when the play function ends
Protected Overrides Sub WndProc(ByRef m As System.Windows.Forms.Message)
     If m.Msg = MM_MCINOTIFY Then
     ' The file is done playing, do whatever is necessary at this point
     MsgBox("Done playing.")
     End If
     MyBase.WndProc(m)
End Sub
```
