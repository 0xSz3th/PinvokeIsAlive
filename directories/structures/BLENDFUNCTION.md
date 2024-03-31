
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct BLENDFUNCTION
{
    public byte BlendOp;
    public byte BlendFlags;
    public byte SourceConstantAlpha;
    public byte AlphaFormat;

    public BLENDFUNCTION(byte op, byte flags, byte alpha, byte format)
    {
        BlendOp = op;
        BlendFlags = flags;
        SourceConstantAlpha = alpha;
        AlphaFormat = format;
    }
}
```

## C# Definition:
```cs
//
// currentlly defined blend operation
//
const int AC_SRC_OVER = 0x00;

//
// currentlly defined alpha format
//
const int AC_SRC_ALPHA = 0x01;
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential)> _
Public Structure BLENDFUNCTION

     Private Shared _BlendOp As Byte
     Private Shared _BlendFlags As Byte
     Private Shared _SourceConstantAlpha As Byte
     Private Shared _AlphaFormat As Byte

     Shared Sub New()
     _BlendOp = 0
     _BlendFlags = 0
     _SourceConstantAlpha = 0
     _AlphaFormat = 0
     End Sub

     Public Property BlendOp As Byte
     Get
         Return _BlendOp
     End Get
     Set(ByVal value As Byte)
         _BlendOp = value
     End Set
     End Property

     Public Property BlendFlags As Byte
     Get
         Return _BlendFlags
     End Get
     Set(ByVal value As Byte)
         _BlendFlags = value
     End Set
     End Property

     Public Property SourceConstantAlpha As Byte
     Get
         Return _SourceConstantAlpha
     End Get
     Set(ByVal value As Byte)
         _SourceConstantAlpha = value
     End Set
     End Property

     Public Property AlphaFormat As Byte
     Get
         Return _AlphaFormat
     End Get
     Set(ByVal value As Byte)
         _AlphaFormat = value
     End Set
     End Property

End Structure
```
