
## C# Definition:
```cs
[ComVisible(true), ComImport()]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [GuidAttribute("7EBFDD87-AD18-11d3-A4C5-00C04F72D6B8")]
    public interface ITravelLogEntry
    {
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetTitle([Out] out IntPtr ppszTitle); //LPOLESTR LPWSTR

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetURL([Out] out IntPtr ppszURL); //LPOLESTR LPWSTR
    }

    [ComVisible(true), ComImport()]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [GuidAttribute("7EBFDD85-AD18-11d3-A4C5-00C04F72D6B8")]
    public interface IEnumTravelLogEntry
    {
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int Next(
        [In, MarshalAs(UnmanagedType.U4)] int celt,
        [Out] out ITravelLogEntry rgelt,
        [Out, MarshalAs(UnmanagedType.U4)] out int pceltFetched);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int Skip([In, MarshalAs(UnmanagedType.U4)] int celt);

    void Reset();

    void Clone([Out] out ITravelLogEntry ppenum);
    }

    public enum TLMENUF
    {
    /// <summary>
    /// Enumeration should include the current travel log entry.
    /// </summary>
    TLEF_RELATIVE_INCLUDE_CURRENT = 0x00000001,
    /// <summary>
    /// Enumeration should include entries before the current entry.
    /// </summary>
    TLEF_RELATIVE_BACK = 0x00000010,
    /// <summary>
    /// Enumeration should include entries after the current entry.
    /// </summary>
    TLEF_RELATIVE_FORE = 0x00000020,
    /// <summary>
    /// Enumeration should include entries which cannot be navigated to.
    /// </summary>
    TLEF_INCLUDE_UNINVOKEABLE = 0x00000040,
    /// <summary>
    /// Enumeration should include all invokable entries.
    /// </summary>
    TLEF_ABSOLUTE = 0x00000031
    }

    [ComVisible(true), ComImport()]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [GuidAttribute("7EBFDD80-AD18-11d3-A4C5-00C04F72D6B8")]
    public interface ITravelLogStg
    {
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int CreateEntry([In, MarshalAs(UnmanagedType.LPWStr)] string pszUrl,
        [In, MarshalAs(UnmanagedType.LPWStr)] string pszTitle, 
        [In] ITravelLogEntry ptleRelativeTo,
        [In, MarshalAs( UnmanagedType.Bool)] bool fPrepend,
        [Out] out ITravelLogEntry pptle);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TravelTo([In] ITravelLogEntry ptle);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int EnumEntries([In] int TLENUMF_flags, [Out] out IEnumTravelLogEntry ppenum);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int FindEntries([In] int TLENUMF_flags,
    [In, MarshalAs( UnmanagedType.LPWStr)] string pszUrl,
    [Out] out IEnumTravelLogEntry ppenum);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetCount([In] int TLENUMF_flags, [Out] out int pcEntries);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int RemoveEntry([In] ITravelLogEntry ptle);

    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetRelativeEntry([In] int iOffset, [Out] out ITravelLogEntry ptle);
    }

    [ComImport, ComVisible(true)]
    [Guid("6d5140c1-7436-11ce-8034-00aa006009fa")]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IServiceProvider
    {
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int QueryService(
        [In] ref Guid guidService,
        [In] ref Guid riid,
        [Out] out IntPtr ppvObject);
    }

    public static Guid IID_ITravelLogStg = new Guid("7EBFDD80-AD18-11d3-A4C5-00C04F72D6B8");
    public static Guid SID_STravelLogCursor = new Guid("7EBFDD80-AD18-11d3-A4C5-00C04F72D6B8");
```

## C# Sample
```cs
public int GetTravelLogStg()
    {
        int iHistoryCount = 0;
        //QI for serviceprovider
       SHDocVw.IWebBrowser2 axWebBrowser = null;
        axWebBrowser = (SHDocVw.IWebBrowser2)webBrowser.ActiveXInstance;
        IServiceProvider psp = axWebBrowser as IServiceProvider;
        if (psp == null)
        return iHistoryCount;

        IntPtr oret = IntPtr.Zero;
        //QueryService for ITravelLogStg
        int hr = psp.QueryService(ref SID_STravelLogCursor, ref IID_ITravelLogStg, out oret);
        if ((oret == IntPtr.Zero) || (hr != Hresults.S_OK))
        return iHistoryCount;

        ITravelLogStg tlstg = Marshal.GetObjectForIUnknown(oret) as ITravelLogStg;
        if (tlstg != null)
        {
        //Get the count
        tlstg.GetCount((int)TLMENUF.TLEF_ABSOLUTE, out iHistoryCount);
        if (iHistoryCount == 0)
            return iHistoryCount;

        Debug.Print("\r\nCount =>" + iHistoryCount.ToString());

        //Enum the travel log entries
        IEnumTravelLogEntry penumtle = null;
        tlstg.EnumEntries((int)TLMENUF.TLEF_ABSOLUTE, out penumtle);
        if (penumtle == null)
            return iHistoryCount;
        hr = 0;
        ITravelLogEntry ptle = null;
        int fetched = 0;
        IntPtr pTitle = IntPtr.Zero;
        IntPtr pUrl = IntPtr.Zero;
        const int MAX_FETCH_COUNT = 1;

        hr = penumtle.Next(MAX_FETCH_COUNT, out ptle, out fetched);
        Marshal.ThrowExceptionForHR(hr);
        //while sucess, continue
        for (int i = 0; Hresults.S_OK == hr; i++)
        {
            if (ptle != null)
            {
            pTitle = IntPtr.Zero;
            pUrl = IntPtr.Zero;
            ptle.GetTitle(out pTitle);
            if (pTitle != IntPtr.Zero)
                Debug.Print("\r\nTitle =>" + Marshal.PtrToStringUni(pTitle));
            ptle.GetURL(out pUrl);
            if (pUrl != IntPtr.Zero)
                Debug.Print("\r\nUrl =>" + Marshal.PtrToStringUni(pUrl));
            }
            hr = penumtle.Next(MAX_FETCH_COUNT, out ptle, out fetched);
            Marshal.ThrowExceptionForHR(hr);
        }
        Marshal.ReleaseComObject(penumtle);
        Marshal.ReleaseComObject(tlstg);
        }
        return iHistoryCount;
    }
```

## VB Definition:
```cs
<ComImport(), _
    ComVisible(False), _
    GuidAttribute("7EBFDD80-AD18-11d3-A4C5-00C04F72D6B8"), _
    InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)> _
Public Interface ITravelLogStg

    <PreserveSig()> _
    Function CreateEntry(<[In](), MarshalAs(UnmanagedType.BStr)> ByVal pszUrl As String, _
    <[In](), MarshalAs(UnmanagedType.BStr)> ByVal pszTitle As String, _
    <[In](), MarshalAs(UnmanagedType.Interface)> ByVal ptleRelativeTo As ITravelLogEntry, _
    <[In](), MarshalAs(UnmanagedType.Bool)> ByVal fPrepend As Boolean, _
    <Out(), MarshalAs(UnmanagedType.Interface)> ByRef pptle As ITravelLogEntry) As Integer

    <PreserveSig()> 
    Function TravelTo(<[In]()> ByVal ptle As ITravelLogEntry) As Integer

    <PreserveSig()> _
    Function EnumEntries(<[In](), MarshalAs(UnmanagedType.U4)> ByVal ptle As TLENUMF, _
    <Out(), MarshalAs(UnmanagedType.Interface)> ByRef ppenum As IEnumTravelLogEntry) As Integer

    <PreserveSig()> _
    Function FindEntries(<[In](), MarshalAs(UnmanagedType.U4)> ByVal flags As TLENUMF, _
    <[In](), MarshalAs(UnmanagedType.BStr)> ByVal pszUrl As String, _
    <Out(), MarshalAs(UnmanagedType.Interface)> ByRef ppenum As IEnumTravelLogEntry) As Integer

    <PreserveSig()> _
    Function GetCount(<[In](), MarshalAs(UnmanagedType.U4)> ByVal flags As TLENUMF, _
    <Out(), MarshalAs(UnmanagedType.U4)> ByRef pcEntries As Integer) As Integer

    <PreserveSig()> _
    Function RemoveEntry(<[In](), MarshalAs(UnmanagedType.Interface)> ByVal ptle As ITravelLogEntry) As Integer

    <PreserveSig()> _
    Function GetRelativeEntry(<[In]()> ByVal iOffset As Integer, _
    <Out(), MarshalAs(UnmanagedType.Interface)> ByRef ptle As ITravelLogEntry) As Integer

End Interface
```
