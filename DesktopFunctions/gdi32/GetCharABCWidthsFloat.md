
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern bool GetCharABCWidthsFloat(IntPtr hdc, uint iFirstChar,
   uint iLastChar, [Out] ABCFLOAT [] lpABCF);
```

## Sample Code:
```cs
/// <summary>The GetCharABCWidthsFloat function retrieves the widths, in logical units, of consecutive
/// characters in a specified range from the current font.</summary>
/// <param name="hdc">Handle to the device context.</param>
/// <param name="iFirstChar">Specifies the code point of the first character in the group of consecutive
/// characters where the ABC widths are seeked.</param>
/// <param name="iLastChar">Specifies the code point of the last character in the group of consecutive
/// characters where the ABC widths are seeked. This range is inclusive. An error is returned if the
/// specified last character precedes the specified first character.</param>
/// <param name="lpABCF">Pointer to an array of ABCFLOAT structures that receives the character widths,
/// in logical units.</param>
/// <remarks>
/// <para>
/// Unlike the GetCharABCWidths function that returns widths only for TrueType fonts, the GetCharABCWidthsFloat 
/// function retrieves widths for any font. The widths returned by this function are in the IEEE floating-point 
/// format. 
/// </para><para>
/// If the current world-to-device transformation is not identified, the returned widths may be noninteger
/// values, even if the corresponding values in the device space are integers.
/// </para><para>
/// A spacing is the distance added to the current position before placing the glyph. B spacing is the width of
/// the black part of the glyph. C spacing is the distance added to the current position to provide white space
/// to the right of the glyph. The total advanced width is specified by A+B+C. 
/// </para><para>
/// The ABC spaces are measured along the character base line of the selected font. 
/// </para><para>
/// The ABC widths of the default character are used for characters outside the range of the currently selected
/// font.
/// </para>
/// </remarks>
/// <returns><para>If the function succeeds, the return value is nonzero.</para>
/// <para>If the function fails, the return value is zero.</para></returns>
[DllImport("gdi32.dll")]
private static extern bool GetCharABCWidthsFloat(IntPtr hdc, uint iFirstChar, uint iLastChar, [Out] ABCFloat[] lpABCF);

/// <summary>Helper methods for fonts to be able to get the widths of each character from the start to the end.</summary>
/// <param name="font"></param>
/// <param name="start"></param>
/// <param name="end"></param>
/// <returns></returns>
public static double[] getCharacterWidths(Font font, uint start, uint end)
{
     IntPtr hDC = GetDC(IntPtr.Zero); //Screen DC
     IntPtr hFont = font.ToHfont();
     IntPtr hObjOld = SelectObject(hDC, hFont);
     ABCFloat[] values = new ABCFloat[end - start];
     GetCharABCWidthsFloat(hDC, start, end, values);
     SelectObject(hDC, hObjOld);
     DeleteObject(hFont);
     ReleaseDC(IntPtr.Zero, hDC); // release that device context.
     //transfer those floats to doubles.
     double[] result = new double[values.Length];
     for (int i = 0; i < values.Length; i++)
     result[i] = values[i].abcfB + ((values[i].abcfA + values[i].abcfC) * 0.5);
     return result;
}

/// <summary>The ABCFLOAT structure contains the A, B, and C widths of a font character.</summary>
/// <remarks>
/// <para>
/// The A, B, and C widths are measured along the base line of the font.
/// </para><para>
/// The character increment (total width) of a character is the sum of the A, B, and C spaces. Either the A or
/// the C space can be negative to indicate underhangs or overhangs. 
/// </para>
/// </remarks>
[StructLayout(LayoutKind.Sequential)]
private struct ABCFloat
{
     /// <summary>Specifies the A spacing of the character. The A spacing is the distance to add to the current
     /// position before drawing the character glyph.</summary>
     public float abcfA;
     /// <summary>Specifies the B spacing of the character. The B spacing is the width of the drawn portion of
     /// the character glyph.</summary>
     public float abcfB;
     /// <summary>Specifies the C spacing of the character. The C spacing is the distance to add to the current
     /// position to provide white space to the right of the character glyph.</summary>
     public float abcfC;
}
```
