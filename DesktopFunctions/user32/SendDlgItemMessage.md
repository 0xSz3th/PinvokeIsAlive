
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr SendDlgItemMessage(IntPtr hDlg, int nIDDlgItem, uint Msg,
   UIntPtr wParam, IntPtr lParam);
```

## VB.Net Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function SendDlgItemMessage(ByVal hDlg As IntPtr, _
                        ByVal nIDDlgItem As Integer, _
                        ByVal Msg As UInteger, _
                        ByVal wParam As UInteger, _
                        ByVal lParam As UInteger) As IntPtr
End Function
```

## VB Signature:
```cs
Private Declare Function SendDlgItemMessage Lib "user32" (ByVal hDlg As IntPtr, _
                               ByVal nIDDlgItem As Integer, _
                               ByVal Msg As UInteger, _
                               ByVal wParam As UInteger, _
                               ByVal lParam As UInteger) As IntPtr
```

## Sample Code:
```cs
Sub ClickSaveBoxNoButton()

    'In this example, we've opened a Notepad instance, entered some text, and clicked the 'X' to close Notepad.
    'Of course we received the 'Do you want to save...' message, and we left it sitting there. Now on to the code...
    '
    'Note: this example also uses API calls to FindWindow, GetDlgItemText, and SetActiveWindow.
    '    You'll have to find those separately.

    'Find the dialog box (no need to find a "parent" first)
    'classname is #32770 (dialog box), dialog box title is Notepad
    Dim theDialogBoxHandle As IntPtr = Nothing
    Dim theDialogBoxClassName As String = "#32770"
    Dim theDialogBoxTitle As String = "Notepad"
    Dim theDialogItemId As Integer = Convert.ToInt32("0xFFFF", 16)
    Dim theDialogTextHolder As New StringBuilder(1000)   'hardcoding capacity - represents maximum text length
    Dim theDialogText As String = String.Empty
    Dim textToLookFor As String = "Do you want to save the changes?"
    Dim isChangeMessage As Boolean = False
    Dim theNoButtonHandle As IntPtr = Nothing
    Dim theNoButtonItemId As Integer = vbNo 'actual Item ID = 7
    Dim theClickMessage As UInteger = Convert.ToUInt32("0x00F5", 16)    '= BM_CLICK value
    Dim wParam As UInteger = 0
    Dim lParam As UInteger = 0

    'Get a dialog box described by the specified info
    theDialogBoxHandle = FindWindow(theDialogBoxClassName, theDialogBoxTitle)
    If theDialogBoxHandle <> IntPtr.Zero Then   'a matching dialog box was found, so continue

        'then get the text
        GetDlgItemText(theDialogBoxHandle, theDialogItemId, theDialogTextHolder, theDialogTextHolder.Capacity)
        theDialogText = theDialogTextHolder.ToString

    End If

    'Make sure it's the right dialog box, based on the text we got.
    isChangeMessage = Regex.IsMatch(theDialogText, textToLookFor)

    If (isChangeMessage) Then

        'Set the dialog box as the active window
        SetActiveWindow(theDialogBoxHandle)

        'And, click the No button
        SendDlgItemMessage(theDialogBoxHandle, theNoButtonItemId, theClickMessage, wParam, lParam)

    End If

    End Sub
```
