
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern int GetClassName(IntPtr hWnd, StringBuilder lpClassName,int nMaxCount);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", CharSet:=CharSet.Auto)> _
Private Shared Function GetClassName(ByVal hWnd As System.IntPtr, _
   ByVal lpClassName As System.Text.StringBuilder, _
   ByVal nMaxCount As Integer) As Integer
    ' Leave function empty     
End Function
```

##  Alternate VB.NET Signature:
```cs
Public Declare Auto Function GetClassName Lib "User32.dll" (ByVal hwnd As IntPtr, _
    <Out()> ByVal lpClassName As System.Text.StringBuilder, _
    ByVal nMaxCount As Integer) As Integer
```

## VB Signature
```cs
Public Declare Function GetClassName Lib "user32" Alias "GetClassNameA" _
         (ByVal hWnd As Long, _
          ByVal lpClassName As String, _
          ByVal nMaxCount As Long) As Long
```

## Sample Code:
```cs
private static bool isIEServerWindow(IntPtr hWnd)
{
    int nRet;
    // Pre-allocate 256 characters, since this is the maximum class name length.
    StringBuilder ClassName = new StringBuilder(256);
    //Get the window class name
    nRet = GetClassName(hWnd, ClassName, ClassName.Capacity);
    if(nRet != 0)
    {
        return (string.Compare(ClassName.ToString(), "Internet Explorer_Server",true,CultureInfo.InvariantCulture) == 0);
    }
    else
    {
        return false;
    }
}
```

## Sample Code:
```cs
Private Sub Button1_Click(ByVal sender As System.Object, _
    ByVal e As System.EventArgs) Handles Button1.Click
   Dim sClassName As New StringBuilder("", 256)
   'pass in the handle of the object for which to get
   'the class name; for example, the form's handle
   Call GetClassName(Me.Handle, sClassName, 256)
   MessageBox.Show(sClassName.ToString) 
End Sub
```
