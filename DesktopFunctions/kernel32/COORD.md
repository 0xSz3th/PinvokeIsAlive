
## C# Signature:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct COORD 
    {
        public short X;
        public short Y;

        public COORD(short X, short Y)
        {
            this.X = X;
            this.Y = Y;
        }
    };
```

## VB Signature:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Public Structure COORD
    Public X As Short
    Public Y As Short

    Public Sub New(ByVal x As Short, ByVal y As Short)
        Me.X = x
        Me.Y = y
    End Sub
    End Structure
```
