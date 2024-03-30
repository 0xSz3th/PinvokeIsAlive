
## C# Signature:
```cs
[DllImport("gdi32.dll", CharSet = CharSet.Auto)]
static extern bool GetTextMetrics(IntPtr hdc, out TEXTMETRIC lptm);

//CharSet.auto automatically selects between these functions based on the OS version:

[DllImport("gdi32.dll", CharSet = CharSet.Unicode)]
private static extern bool GetTextMetricsW(IntPtr hdc, out TEXTMETRICW lptm);

[DllImport("gdi32.dll", CharSet = CharSet.Ansi)]
private static extern bool GetTextMetricsA(IntPtr hdc, out TEXTMETRICA lptm);
```

## Sample Code:
```cs
public static TEXTMETRIC GetTextMetrics(Graphics graphics, Font font) 
{ 
   IntPtr hDC = graphics.GetHdc(); 
   TEXTMETRIC textMetric; 
   IntPtr hFont = font.ToHfont(); 
   try 
   { 
     IntPtr hFontPreviouse = SelectObject(hDC, hFont); 
     bool result = GetTextMetrics(hDC, out textMetric); 
     SelectObject(hDC, hFontPreviouse); 
   } 
   finally 
   {  
     DeleteObject(hFont); 
     graphics.ReleaseHdc(hDC); 
   } 
   return textMetric; 
} 

[DllImport("Gdi32.dll", CharSet=CharSet.Auto)] 
static extern IntPtr SelectObject(IntPtr hdc, IntPtr hgdiobj); 

[DllImport("Gdi32.dll", CharSet=CharSet.Auto)] 
static extern bool GetTextMetrics(IntPtr hdc, out TEXTMETRIC lptm); 

[DllImport("Gdi32.dll", CharSet=CharSet.Auto)] 
static extern bool DeleteObject(IntPtr hdc); 

[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Auto)]
internal struct TEXTMETRIC
{
   public int tmHeight;
   public int tmAscent;
   public int tmDescent;
   public int tmInternalLeading;
   public int tmExternalLeading;
   public int tmAveCharWidth;
   public int tmMaxCharWidth;
   public int tmWeight;
   public int tmOverhang;
   public int tmDigitizedAspectX;
   public int tmDigitizedAspectY;
   public char tmFirstChar;
   public char tmLastChar;
   public char tmDefaultChar;
   public char tmBreakChar;
   public byte tmItalic;
   public byte tmUnderlined;
   public byte tmStruckOut;
   public byte tmPitchAndFamily;
   public byte tmCharSet;
}

// C++/CLI

[StructLayout(LayoutKind::Sequential, CharSet=CharSet::Unicode)]
public ref struct TEXTMETRIC
{
   int tmHeight;
   int tmAscent;
   int tmDescent;
   int tmInternalLeading;
   int tmExternalLeading;
   int tmAveCharWidth;
   int tmMaxCharWidth;
   int tmWeight;
   int tmOverhang;
   int tmDigitizedAspectX;
   int tmDigitizedAspectY;
   Char tmFirstChar;
   Char tmLastChar;
   Char tmDefaultChar;
   Char tmBreakChar;
   Byte tmItalic;
   Byte tmUnderlined;
   Byte tmStruckOut;
   Byte tmPitchAndFamily;
   Byte tmCharSet;
};

[DllImport("Gdi32.dll", CharSet=CharSet::Unicode)]
static bool GetTextMetrics(IntPtr hdc, [Out] TEXTMETRIC% lptm); 

TEXTMETRIC^ GetTextMetricsReal(Graphics^ g, Font^ font)
{
   IntPtr hDC = g->GetHdc();
   TEXTMETRIC^ textMetric = gcnew TEXTMETRIC;
   IntPtr hFont = font->ToHfont();
   try
   {
      IntPtr hFontPrevious = Win32::SelectObject(hDC, hFont);
      bool result = Win32::GetTextMetrics(hDC, *textMetric);
      Win32::SelectObject(hDC, hFontPrevious);
   }
   finally
   {  
      Win32::DeleteObject(hFont);
      g->ReleaseHdc(hDC);
   }

   return textMetric;
}
```
