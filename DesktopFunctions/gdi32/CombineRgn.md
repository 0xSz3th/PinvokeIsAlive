
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int CombineRgn(IntPtr hrgnDest, IntPtr hrgnSrc1,
   IntPtr hrgnSrc2, int fnCombineMode);
```

## User-Defined Types:
```cs
public enum CombineRgnStyles:int
{
    RGN_AND         =1,
    RGN_OR          =2,
    RGN_XOR         =3,
    RGN_DIFF        =4,
    RGN_COPY        =5,
    RGN_MIN         =RGN_AND,
    RGN_MAX         =RGN_COPY
}
```

## Return Values:
```cs
public const int ERROR = 0;
public const int NULLREGION = 1;
public const int SIMPLEREGION = 2;
public const int COMPLEXREGION = 3;
```

## Sample Code:
```cs
[DllImport("gdi32.dll")]
    public static extern IntPtr CreateEllipticRgn(int nLeftRect, int nTopRect,int nRightRect, int nBottomRect);

    [DllImport("user32.dll")]
    static extern System.UInt16  SetWindowRgn(IntPtr hWnd, IntPtr hRgn, bool bRedraw);

    [DllImport("gdi32.dll")]
    static extern int CombineRgn(IntPtr hrgnDest, IntPtr hrgnSrc1,IntPtr hrgnSrc2, int fnCombineMode);
```

## Sample Code:
```cs
// And the code lies here
```

## Sample Code:
```cs
IntPtr r1 = CreateEllipticRgn(0,0,300,300);
            IntPtr r2 = CreateEllipticRgn(100,100,300,300);
            IntPtr r3= CreateEllipticRgn(100,100,300,300);
            CombineRgn(r3,r1,r2,0);
            SetWindowRgn(this.Handle,r3,true);
```
