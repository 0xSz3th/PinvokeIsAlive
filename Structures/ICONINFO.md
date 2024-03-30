
## C# Definition:
```cs
struct ICONINFO
{
    /// <summary>
    /// Specifies whether this structure defines an icon or a cursor.
    /// A value of TRUE specifies an icon; FALSE specifies a cursor
    /// </summary>
    bool fIcon;
    /// <summary>
    /// The x-coordinate of a cursor's hot spot
    /// </summary>
    Int32 xHotspot;
    /// <summary>
    /// The y-coordinate of a cursor's hot spot
    /// </summary>
    Int32 yHotspot;
    /// <summary>
    /// The icon bitmask bitmap
    /// </summary>
    IntPtr hbmMask;
    /// <summary>
    /// A handle to the icon color bitmap. 
    /// </summary>
    IntPtr hbmColor;
}
```

## VB Definition:
```cs
Structure ICONINFO 
   ''' <summary>
   ''' Specifies whether this structure defines an icon or a cursor.
   ''' A value of TRUE specifies an icon; FALSE specifies a cursor.
   ''' </summary>
   Public fIcon As Boolean

   ''' <summary>
   ''' The x-coordinate of a cursor's hot spot.
   ''' </summary>
   Public xHotspot As Integer

   ''' <summary>
   ''' The y-coordinate of the cursor's hot spot.
   ''' </summary>
   Public yHotspot As Integer

   ''' <summary>
   ''' The icon bitmask bitmap.
   ''' </summary>
   Public hbmMask As IntPtr

   ''' <summary>
   ''' A handle to the icon color bitmap.
   ''' </summary>
   Public hbmColor As IntPtr
End Structure
```
