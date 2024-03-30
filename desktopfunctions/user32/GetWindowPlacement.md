
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool GetWindowPlacement(IntPtr hWnd, ref WINDOWPLACEMENT lpwndpl);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function GetWindowPlacement(ByVal hWnd As IntPtr, ByRef lpwndpl As WINDOWPLACEMENT) As Boolean
End Function
```

## VB Signature:
```cs
Public Declare Function GetWindowPlacement Lib "user32" _
          (ByVal hWnd As Long, _
           ByRef lpwndpl As WINDOWPLACEMENT) As Long
```

## C# Sample Code:
```cs
private void GetPlacement()
{
        WINDOWPLACEMENT placement = new WINDOWPLACEMENT();
        placement.length = Marshal.SizeOf(placement);
        GetWindowPlacement(this.Handle, ref placement);
}
```

## VB Sample Code:
```cs
Public Class Form1

    Private Declare Function GetWindowPlacement Lib "user32" (ByVal hwnd As IntPtr, ByRef lpwndpl As WINDOWPLACEMENT) As Integer

    Private Structure POINTAPI
         Public x As Integer
         Public y As Integer
    End Structure

    Private Structure RECT
         Public Left As Integer
         Public Top As Integer
         Public Right As Integer
         Public Bottom As Integer
    End Structure

    Private Structure WINDOWPLACEMENT
         Public Length As Integer
         Public flags As Integer
         Public showCmd As Integer
         Public ptMinPosition As POINTAPI
         Public ptMaxPosition As POINTAPI
         Public rcNormalPosition As RECT
    End Structure


    Private Sub Form1_Click(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Click

        Dim intRet As Integer
        Dim wpTemp As WINDOWPLACEMENT

        wpTemp.Length = System.Runtime.InteropServices.Marshal.SizeOf(wpTemp)
        intRet = GetWindowPlacement(Me.Handle.ToInt32, wpTemp)

        If wpTemp.showCmd = 1 Then
            'normal
        ElseIf wpTemp.showCmd = 2 Then
            'minimized
        ElseIf wpTemp.showCmd = 3 Then
            'maximized
        End If
        'Stop

    End Sub

End Class
```
