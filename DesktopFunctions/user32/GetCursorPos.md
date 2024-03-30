[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool GetCursorPos(out POINT point);
[StructLayout(LayoutKind.Sequential)]
struct POINT
  {
    public Int32 X;
    public Int32 Y;
}
<DllImport("user32.dll", ExactSpelling := True, SetLastError := True)> _
    Public Shared Function GetCursorPos(ByRef lpPoint As POINT) As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
Declare Function GetCursorPos Lib "user32.dll" _
   (ByRef lpPoint As POINT) as boolean

<DllImport("user32.dll")> _
   Public Function GetCursorPos(<[In](), Out()> ByRef pt As POINT) As Boolean
   End Function

## Point declaration
```cs
<System.Runtime.InteropServices.StructLayout(Runtime.InteropServices.LayoutKind.Sequential)> _
   Public Structure POINT
      Public X As Integer
      Public Y As Integer

      Public Sub New(ByVal X As Integer, ByVal Y As Integer)
     Me.X = X
     Me.Y = Y
      End Sub
   End Structure
```

## Tips & Tricks:
```cs
POINT p;
if (GetCursorPos(out p))
{
    label1.Text = Convert.ToString(p.X) + ";" + Convert.ToString(p.Y);
}
```

## Tips & Tricks:
```cs
[StructLayout(LayoutKind.Sequential)]
    struct POINT
    {
        public Int32 X;
        public Int32 Y;
    }

    [DllImport("user32.dll")]
    [return: MarshalAs(UnmanagedType.Bool)]
    static extern bool GetCursorPos(out POINT point);

    static void Main(string[] args)
    {
        POINT p = new POINT();
        GetCursorPos(out p);

        Console.WriteLine(p.X);
        Console.WriteLine(p.Y);
        Console.ReadLine();
    }
```

## Alternative Managed API:
```cs
System.Windows.Forms.Cursor.Position
```
