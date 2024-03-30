
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.U2)]
static extern short RegisterClassEx([In] ref WNDCLASSEX lpwcx);
```

## VB Signature:
```cs
<DllImport("user32.dll")> _
Public Shared Function RegisterClassEx(ByRef lpwcx As WNDCLASSEX) As Short
End Function
```

## Sample Code(VB.NET):
```cs
<StructLayout(LayoutKind.Sequential)> _
    Private Structure WNDCLASSEX
        Public cbSize As UInteger
        Public style As ClassStyles
        Public lpfnWndProc As IntPtr
        Public cbClsExtra As Integer
        Public cbWndExtra As Integer
        Public hInstance As IntPtr
        Public hIcon As IntPtr
        Public hCursor As IntPtr
        Public hbrBackground As IntPtr
        Public lpszMenuName As String
        Public lpszClassName As String
        Public hIconSm As IntPtr

        Shared Function MakeNew()
        Dim nw As New WNDCLASSEX
        nw.cbSize = Marshal.SizeOf(GetType(WNDCLASSEX))
        Return nw
        End Function
    End Structure

    <DllImport("user32.dll")> _
    Private Shared Function RegisterClassEx(ByRef lpwcx As WNDCLASSEX) As Short
    End Function

    <DllImport("user32.dll")> _
    Private Shared Function UnregisterClass(lpClassName As String, hInstance As IntPtr) As Boolean
    End Function

    Dim className As String = "Iranian_Persian_Class"
    Dim WndClass As WNDCLASSEX = WNDCLASSEX.MakeNew()
    With WndClass
        .style = 0
        .lpfnWndProc = IntPtr.Zero
        .cbClsExtra = 0
        .cbWndExtra = 0
        .hInstance = IntPtr.Zero
        .hIcon = IntPtr.Zero
        .hCursor = IntPtr.Zero
        .hbrBackground = IntPtr.Zero
        .lpszMenuName = ""
        .lpszClassName = className
        .hIconSm = IntPtr.Zero
    End With

    Dim rVal As Short = RegisterClassEx(WndClass)
    If rVal = 0 Then
        MsgBox("an error occured")
    Else
        With WndClass
        MsgBox("Class atom: " & rVal.ToString & vbCrLf & _
               "cbClsExtra: " & .cbClsExtra.ToString & vbCrLf & _
               "cbSize: " & .cbSize.ToString & vbCrLf & _
               "cbWndExtra: " & .cbWndExtra.ToString & vbCrLf & _
               "hbrBackground: " & .hbrBackground.ToString & vbCrLf & _
               "hCursor: " & .hCursor.ToString & vbCrLf & _
               "hIcon: " & .hIcon.ToString & vbCrLf & _
               "hIconSm: " & .hIconSm.ToString & vbCrLf & _
               "hInstance: " & .hInstance.ToString & vbCrLf & _
               "lpfnWndProc: " & .lpfnWndProc.ToString & vbCrLf & _
               "lpszClassName: " & .lpszClassName.ToString & vbCrLf & _
               "lpszMenuName: " & .lpszMenuName.ToString & vbCrLf & _
               "style: " & .style.ToString)
        End With

        If UnregisterClass(WndClass.lpszClassName, WndClass.hInstance) Then
        MsgBox("Unregister Class Sucessfuly")
        Else
        MsgBox("Unregister Class Failed")
        End If
    End If
```
