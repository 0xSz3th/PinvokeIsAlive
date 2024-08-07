
## C# Definition:
```cs
[StructLayout (LayoutKind.Sequential, CharSet=CharSet.Unicode)]
struct DESKBANDINFO {
    /// <summary>
    /// Set of flags that determine which members of this structure are being requested. 
    /// </summary>
    /// <remarks>
    /// This will be a combination of the following values:
    ///     DBIM_MINSIZE    ptMinSize is being requested.
    ///     DBIM_MAXSIZE    ptMaxSize is being requested.
    ///     DBIM_INTEGRAL   ptIntegral is being requested.
    ///     DBIM_ACTUAL     ptActual is being requested.
    ///     DBIM_TITLE      wszTitle is being requested.
    ///     DBIM_MODEFLAGS  dwModeFlags is being requested.
    ///     DBIM_BKCOLOR    crBkgnd is being requested.
    /// </remarks>
    public DBIM dwMask;
    /// <summary>
    /// Point structure that receives the minimum size of the band object. 
    /// The minimum width is placed in the x member and the minimum height 
    /// is placed in the y member. 
    /// </summary>
    public Point ptMinSize;
    /// <summary>
    /// Point structure that receives the maximum size of the band object. 
    /// The maximum height is placed in the y member and the x member is ignored. 
    /// If there is no limit for the maximum height, (LONG)-1 should be used. 
    /// </summary>
    public Point ptMaxSize;
    /// <summary>
    /// Point structure that receives the sizing step value of the band object. 
    /// The vertical step value is placed in the y member, and the x member is ignored. 
    /// The step value determines in what increments the band will be resized. 
    /// </summary>
    /// <remarks>
    /// This member is ignored if dwModeFlags does not contain DBIMF_VARIABLEHEIGHT. 
    /// </remarks>
    public Point ptIntegral;
    /// <summary>
    /// Point structure that receives the ideal size of the band object. 
    /// The ideal width is placed in the x member and the ideal height is placed in the y member. 
    /// The band container will attempt to use these values, but the band is not guaranteed to be this size.
    /// </summary>
    public Point ptActual;
    /// <summary>
    /// The title of the band.
    /// </summary>
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 255)]
    public String wszTitle;
    /// <summary>
    /// A value that receives a set of flags that define the mode of operation for the band object. 
    /// </summary>
    /// <remarks>
    /// This must be one or a combination of the following values.
    ///     DBIMF_NORMAL
    ///     The band is normal in all respects. The other mode flags modify this flag.
    ///     DBIMF_VARIABLEHEIGHT
    ///     The height of the band object can be changed. The ptIntegral member defines the 
    ///     step value by which the band object can be resized. 
    ///     DBIMF_DEBOSSED
    ///     The band object is displayed with a sunken appearance.
    ///     DBIMF_BKCOLOR
    ///     The band will be displayed with the background color specified in crBkgnd.
    /// </remarks>
    public DBIMF dwModeFlags;
    /// <summary>
    /// The background color of the band.
    /// </summary>
    /// <remarks>
    /// This member is ignored if dwModeFlags does not contain the DBIMF_BKCOLOR flag. 
    /// </remarks>
    public Int32 crBkgnd; 
}
```

## VB Definition:
```cs
Structure DESKBANDINFO 
   Public TODO
End Structure
```
