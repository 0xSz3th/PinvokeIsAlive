
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct OBJECTDESCRIPTOR
{
    public OBJECTDESCRIPTOR ()
    {
    }

    public uint cbSize; 
    public Guid clsid; 
    public DVASPECT dwDrawAspect; 
    public Size  sizel; 
    public Point pointl; 
    public int dwStatus; 
    public int dwFullUserTypeName; 
    public int dwSrcOfCopy; 
    /* variable sized string data may appear here */ 
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)>
Public Class OBJECTDESCRIPTOR

     Public Sub New()

     End Sub
     Public cbSize As UInteger
     Public clsid As Guid
     Public dwDrawAspect As DVASPECT
     Public sizel As Size
     Public pointl As Point
     Public dwStatus As Integer
     Public dwFullUserTypeName As Integer
     Public dwSrcOfCopy As Integer
     ' variable sized string data may appear here
End Class
```

## Notes:
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
    }

    [StructLayout(LayoutKind.Sequential)]
    public struct SIZE
    {
    public int cx;
    public int cy;

    public SIZE(int cx, int cy)
    {
        this.cx = cx;
        this.cy = cy;
    }
    }
```

## Notes:
```cs
///// <summary>
    ///// The DVASPECT enumeration values specify the desired data or view aspect of the object when drawing or getting data.
    ///// </summary>
    [Flags]
    public enum DVASPECT
    {
    DVASPECT_CONTENT = 1,
    DVASPECT_THUMBNAIL = 2,
    DVASPECT_ICON = 4,
    DVASPECT_DOCPRINT = 8
    }
```
