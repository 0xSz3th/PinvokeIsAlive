
## C# Signature:
```cs
[DllImport("user32.dll", CharSet = CharSet.Auto)]
public static extern IntPtr SendMessage(IntPtr hWnd, uint Msg, uint wParam, StringBuilder lParam);

[DllImport("user32.dll", CharSet = CharSet.Auto)]
public static extern IntPtr SendMessage(IntPtr hWnd, uint Msg, uint wParam, [MarshalAs(UnmanagedType.LPWStr)] string lParam);

[DllImport("user32.dll", CharSet = CharSet.Auto)]
public static extern IntPtr SendMessage(IntPtr hWnd, uint Msg, uint wParam, [MarshalAs(UnmanagedType.LPWStr)] string lParam);

[DllImport("user32.dll", CharSet = CharSet.Auto)]
public static extern IntPtr SendMessage(IntPtr hWnd, uint Msg, uint wParam, ref uint lParam);

[DllImport("user32.dll", CharSet = CharSet.Auto)]
public static extern IntPtr SendMessage(IntPtr hWnd, uint Msg, uint wParam, uint lParam);
```

## VB Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)>
Public Shared Function SendMessage(ByVal hWnd As IntPtr, ByVal Msg As Integer, ByVal wParam As IntPtr, ByVal lParam As StringBuilder) As IntPtr
End Function

<DllImport("user32.dll", CharSet:=CharSet.Auto)>
Public Shared Function SendMessage(ByVal hWnd As IntPtr, ByVal Msg As Integer, ByVal wParam As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> ByVal lParam As String) As IntPtr
End Function

<DllImport("user32.dll", CharSet:=CharSet.Auto)>
Public Shared Function SendMessage(ByVal hWnd As IntPtr, ByVal Msg As Integer, ByVal wParam As Integer, <MarshalAs(UnmanagedType.LPWStr)> ByVal lParam As String) As IntPtr
End Function

<DllImport("user32.dll", CharSet:=CharSet.Auto)>
Public Shared Function SendMessage(ByVal hWnd As IntPtr, ByVal Msg As Integer, ByVal wParam As Integer, ByRef lParam As IntPtr) As IntPtr
End Function

<DllImport("user32.dll", CharSet:=CharSet.Auto)>
Public Shared Function SendMessage(ByVal hWnd As IntPtr, ByVal Msg As Integer, ByVal wParam As Integer, ByVal lParam As IntPtr) As IntPtr
End Function
```

## Sample Code:
```cs
//Set a note to a CommandLink
SendMessage(myCommandLink, BCM_SETNOTE, 0, "My CommandLink Note");

//Retrieve a text using WM_GETTEXT
int length = SendMessage(myHwndHandle, WM_GETTEXTLENGTH, 0, 0).ToInt32();
StringBuilder builder = new StringBuilder(length);
SendMessage(myHwndHandle, WM_GETTEXT, length, builder);
```

## Sample Code:
```cs
Dim length As Integer = SendMessage(hWnd, WM_GETTEXTLENGTH, 0, 0)
    Dim title As New String(New Char, length)
    SendMessage(hWnd, WM_GETTEXT, length+1, title)
    Return title
```
