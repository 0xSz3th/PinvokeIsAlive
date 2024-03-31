
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
public class IMAGEINFO
{
      public IntPtr hbmImage;
      public IntPtr hbmMask;
      public int Unused1;
      public int Unused2;
      public int rcImage_left;
      public int rcImage_top;
      public int rcImage_right;
      public int rcImage_bottom;
      public IMAGEINFO();
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Sequential, Pack=1)> _ 
Public Class IMAGEINFO
      Public hbmImage As IntPtr
      Public hbmMask As IntPtr
      Public Unused1 As Integer
      Public Unused2 As Integer
      Public rcImage_left As Integer
      Public rcImage_top As Integer
      Public rcImage_right As Integer
      Public rcImage_bottom As Integer
      Public IMAGEINFO()
End Class
```
