
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct POINT
    {
        public int X;
        public int Y;

        public POINT(int x, int y)
        {
            this.X = x;
            this.Y = y;
        }

        public static implicit operator System.Drawing.Point(POINT p)
        {
            return new System.Drawing.Point(p.X, p.Y);
        }

        public static implicit operator POINT(System.Drawing.Point p)
        {
            return new POINT(p.X, p.Y);
        }

        public override string ToString()
        {
            return $"X: {X}, Y: {Y}";
        }
    }
```

## VB .NET Signature:
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

## VB Signature
```cs
Public Type POINT
    X As Long
    Y As Long
End Type
```

## Notes:
```cs
public const int PM_NOREMOVE = 0x0000;
  public const int PM_REMOVE = 0x0001;
  public const int PM_NOYIELD = 0x0002;
```
