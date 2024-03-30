
## C# Signature:
```cs
[DllImport("uxtheme", ExactSpelling=true, CharSet=CharSet.Unicode)]
public extern static Int32 GetThemeFilename(IntPtr hTheme, int iPartId, int iStateId, int iPropId, StringBuilder themeFileName, int themeFileNameLength);
```

## VB .NET Signature:
```cs
Declare Auto Function GetThemeFilename Lib "uxtheme.dll" (hTheme as IntPtr, iPartId as Integer, iStateId as Integer, themeFileName as Integer, themeFileNameLength as Integer) As Integer
```

## Parameters
```cs
hTheme
    [in] Handle to a window's specified theme data. Use OpenThemeData to create an HTHEME.
    iPartId
    [in] Value of type int that specifies the part that contains the filename property. See Parts and States. 
    iStateId
    [in] Value of type int that specifies the state of the part. See Parts and States.
    iPropId
    [in] Value of type int that specifies the property to retrieve. May be one of the following values.

    TMT_IMAGEFILE
        The filename of the image associated with this part and state, or the base filename for multiple images associated with this part and state.
    TMT_IMAGEFILE1
        The filename of the first scaled image associated with this part and state, for support of different resolutions.
    TMT_IMAGEFILE2
        The filename of the second scaled image.
    TMT_IMAGEFILE3
        The filename of the third scaled image.
    TMT_IMAGEFILE4
        The filename of the fourth scaled image.
    TMT_IMAGEFILE5
        The filename of the fifth scaled image.
    TMT_STOCKIMAGEFILE
        Not used.
    TMT_GLYPHIMAGEFILE
        The filename for the glyph image associated with this part and state.

    pszThemeFilename
    [out] Pointer to a buffer that receives the retrieved file name.
    cchMaxBuffChars
    [in] Value of type int that receives the maximum number of characters in the file name
```
