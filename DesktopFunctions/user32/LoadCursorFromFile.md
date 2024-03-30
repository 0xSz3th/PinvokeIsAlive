
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern IntPtr LoadCursorFromFile(string lpFileName);
```

## VB.Net Signature
```cs
<DllImport("user32.dll")> _
    Private Shared Function LoadCursorFromFile(ByVal lpFileName As String) As IntPtr
    End Function
```

## Sample Code C#:
```cs
private void Surface_MouseEnter(object sender, EventArgs e)
    {//Assuming you have declared the function using the C# signature above, and have a control / form /etc with a MouseEnter handled by this function

        //Assumes that a file (in this case a pencil cursor - PencilCursor.cur) is in Application.StartupPath (in debug mode that's app folder/bin/debug
        Cursor myCursor = new Cursor(GetType(), "PencilCursor.cur"); 
        IntPtr colorCursorHandle = LoadCursorFromFile("PencilCursor.cur");
        myCursor.GetType().InvokeMember("handle",BindingFlags.Public | BindingFlags.NonPublic |BindingFlags.Instance | System.Reflection.BindingFlags.SetField,null,myCursor,new object [] { colorCursorHandle } );
        this.Cursor = myCursor;
    }
```

##  Sample Code VB.Net
```cs
<DllImport("user32.dll")> _
    Private Shared Function DestroyCursor(ByVal hCursor As IntPtr) As Integer
    End Function

    <DllImport("user32.dll")> _
    Private Shared Function LoadCursorFromFile(ByVal lpFileName As String) As IntPtr
    End Function

    Dim mhAniCursor As IntPtr

    Private Sub Form_Closed(ByVal sender As System.Object, ByVal e As FormClosedEventArgs) Handles MyBase.FormClosed
    'Animierten  bzw. farbigen Cursor entladen
    Dim iResult As Integer = DestroyCursor(mhAniCursor)
    End Sub

    Private Sub Form1_Load(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles MyBase.Load
    mhAniCursor = LoadCursorFromFile("c:\FarbCursor.cur")
    If Not mhAniCursor.Equals(IntPtr.Zero) Then
        Me.Cursor = New Cursor(mhAniCursor)
    End If
    End Sub
```
