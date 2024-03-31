
## C# Definition:
```cs
[return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int SetSecuritySite([In] IntPtr pSite);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int GetSecuritySite([Out] IntPtr pSite);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int MapUrlToZone([In,MarshalAs(UnmanagedType.LPWStr)] string pwszUrl, 
           ref UInt32 pdwZone, UInt32 dwFlags);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int GetSecurityId([MarshalAs(UnmanagedType.LPWStr)] string pwszUrl, 
            [MarshalAs(UnmanagedType.LPArray)] byte[] pbSecurityId, 
            ref UInt32  pcbSecurityId, uint dwReserved);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int ProcessUrlAction([In,MarshalAs(UnmanagedType.LPWStr)] string pwszUrl, 
               UInt32 dwAction, out byte pPolicy, UInt32 cbPolicy, 
               byte pContext, UInt32 cbContext, UInt32 dwFlags, 
               UInt32 dwReserved);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int QueryCustomPolicy([In,MarshalAs(UnmanagedType.LPWStr)] string pwszUrl,  
            ref Guid guidKey, ref byte ppPolicy, ref UInt32 pcbPolicy,
            ref byte pContext, UInt32 cbContext, UInt32 dwReserved);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int SetZoneMapping(UInt32 dwZone, 
             [In,MarshalAs(UnmanagedType.LPWStr)] string lpszPattern, 
             UInt32 dwFlags);

  [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
  int GetZoneMappings(UInt32 dwZone, out UCOMIEnumString ppenumString, 
              UInt32 dwFlags);
```

## C# Sample Application:
```cs
[ComImport, GuidAttribute("79EAC9EE-BAF9-11CE-8C82-00AA004BA90B")]
  [InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
  public interface IInternetSecurityManager
  {
    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int SetSecuritySite([In] IntPtr pSite);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int GetSecuritySite([Out] IntPtr pSite);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int MapUrlToZone([In,MarshalAs(UnmanagedType.LPWStr)] string pwszUrl, 
             out UInt32 pdwZone, UInt32 dwFlags);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int GetSecurityId([MarshalAs(UnmanagedType.LPWStr)] string pwszUrl, 
              [MarshalAs(UnmanagedType.LPArray)] byte[] pbSecurityId, 
              ref UInt32  pcbSecurityId, uint dwReserved);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int ProcessUrlAction([In,MarshalAs(UnmanagedType.LPWStr)] string pwszUrl, 
             UInt32 dwAction, out byte pPolicy, UInt32 cbPolicy, 
             byte pContext, UInt32 cbContext, UInt32 dwFlags, 
             UInt32 dwReserved);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int QueryCustomPolicy([In,MarshalAs(UnmanagedType.LPWStr)] string pwszUrl,  
              ref Guid guidKey, ref byte ppPolicy, ref UInt32 pcbPolicy,
              ref byte pContext, UInt32 cbContext, UInt32 dwReserved);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int SetZoneMapping(UInt32 dwZone, 
               [In,MarshalAs(UnmanagedType.LPWStr)] string lpszPattern, 
               UInt32 dwFlags);

    [return: MarshalAs(UnmanagedType.I4)][PreserveSig]
    int GetZoneMappings(UInt32 dwZone, out UCOMIEnumString ppenumString, 
            UInt32 dwFlags);
  }

  [ComImport, GuidAttribute("6D5140C1-7436-11CE-8034-00AA006009FA")]
  [InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
  public interface IServiceProvider
  {
    void QueryService(ref Guid guidService, ref Guid riid, 
              [MarshalAs(UnmanagedType.Interface)] out object ppvObject);
  }

  [Guid("<interface guid>")]
  [InterfaceType(ComInterfaceType.InterfaceIsIDispatch)]
  public interface _ZoneSecurityDemo
  {
    [DispId(1)]
    void AssessZoneSafety();
  }
```

## C# Sample Application:
```cs
[Guid("<class guid>")]
  [ClassInterface(ClassInterfaceType.None)]
  [ProgId("IEZoneSecurity.ZoneSecurityDemo")]
  public class ZoneSecurityDemo : System.Windows.Forms.Control, _ZoneSecurityDemo
  {
    private Guid _IID_TopLevelBrowser = new Guid("4C96BE40-915C-11CF-99D3-00AA004AE837");
    private Guid _IID_WebBrowserApp = new Guid("0002DF05-0000-0000-C000-000000000046");
    private Guid _CLSID_SecurityManager = new Guid("7b8a2d94-0ac9-11d1-896c-00c04fb6bfc4");

    private bool _ZoneSafetyConfirmed = false;

    public void AssessZoneSafety()
    {
      object oleClientSiteObj = null;
      IEZoneSecurity.IServiceProvider serviceProvider = null;
      object topServiceProviderObj = null;
      IServiceProvider topServiceProvider = null;
      object webBrowserObj = null;
      SHDocVw.IWebBrowser webBrowser = null;
      try
      {
    // Get the client site service provider.
    Type iOleObjectType = this.GetType().GetInterface("IOleObject", true);
    oleClientSiteObj = iOleObjectType.InvokeMember("GetClientSite",
                               BindingFlags.Instance | 
                               BindingFlags.InvokeMethod |
                               BindingFlags.Public, null,
                               this, null);
    serviceProvider = oleClientSiteObj as IEZoneSecurity.IServiceProvider;

    // Get top level browser service provider.
    Guid IID_TopLevelBrowser = _IID_TopLevelBrowser;
    Guid Riid = typeof(IEZoneSecurity.IServiceProvider).GUID;
    topServiceProviderObj = null;
    serviceProvider.QueryService(ref IID_TopLevelBrowser, ref Riid, 
                     out topServiceProviderObj);
    topServiceProvider = topServiceProviderObj as IServiceProvider;

    // Get web browser object.
    Guid IID_WebBrowserApp = _IID_WebBrowserApp;
    Riid = typeof(SHDocVw.IWebBrowser).GUID;
    webBrowserObj = null;
    topServiceProvider.QueryService(ref IID_WebBrowserApp, ref Riid,
                    out webBrowserObj);
    webBrowser = webBrowserObj as SHDocVw.IWebBrowser;

    // Determine which zone the browser is currently in.
    Type t = Type.GetTypeFromCLSID(_CLSID_SecurityManager);
    object securityManager = Activator.CreateInstance(t);
    IInternetSecurityManager ISM = securityManager as IInternetSecurityManager;
    uint Zone;
    ISM.MapUrlToZone(webBrowser.LocationURL, out Zone, 0);
    Marshal.ReleaseComObject(securityManager);

    // Only accept calls from the My Computer zone.
    if (Zone == 0)
      _ZoneSafetyConfirmed = true;
      }
      catch
      {
      }
      finally
      {
    if (webBrowser != null)
      Marshal.ReleaseComObject(webBrowser);
    if (webBrowserObj != null)
      Marshal.ReleaseComObject(webBrowserObj);
    if (topServiceProvider != null)
      Marshal.ReleaseComObject(topServiceProvider);
    if (topServiceProviderObj != null)
      Marshal.ReleaseComObject(topServiceProviderObj);
    if (serviceProvider!= null)
      Marshal.ReleaseComObject(serviceProvider);
    if (oleClientSiteObj != null)
      Marshal.ReleaseComObject(oleClientSiteObj);
      }
    }
  }
```

## VB Definition:
```cs
<ComImport(), GuidAttribute("79EAC9EE-BAF9-11CE-8C82-00AA004BA90B")> _
   <InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)> _
   Public Interface IInternetSecurityManager
    <PreserveSig()> _
    Function SetSecuritySite(<[In]()> ByVal pSite As IntPtr) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function GetSecuritySite(<[Out]()> ByVal pSite As IntPtr) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function MapUrlToZone(<[In]()> <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszUrl As String,
       ByRef pdwZone As UInt32, ByVal dwFlags As UInt32) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function GetSecurityId(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszUrl As String,
        <MarshalAs(UnmanagedType.LPArray)> ByVal pbSecurityId As Byte(),
        ByRef pcbSecurityId As UInt32, ByVal dwReserved As UInt32) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function ProcessUrlAction(<[In]()> <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszUrl As String,
           ByVal dwAction As UInt32, <[Out]()> ByVal pPolicy As Byte, ByVal cbPolicy As UInt32,
           ByVal pContext As Byte, ByVal cbContext As UInt32, ByVal dwFlags As UInt32,
           ByVal dwReserved As UInt32) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function QueryCustomPolicy(<[In]()> <MarshalAs(UnmanagedType.LPWStr)> ByVal pwszUrl As String,
        ByRef guidKey As Guid, ByRef ppPolicy As Byte, ByRef pcbPolicy As UInt32,
        ByRef pContext As Byte, ByVal cbContext As UInt32, ByVal dwReserved As UInt32) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function SetZoneMapping(ByVal dwZone As UInt32,
         <[In]()> <MarshalAs(UnmanagedType.LPWStr)> ByVal lpszPattern As String,
         ByVal dwFlags As UInt32) As <MarshalAs(UnmanagedType.I4)> Integer

    <PreserveSig()> _
    Function GetZoneMappings(ByVal dwZone As UInt32, <[Out]()> ByVal ppenumString As IEnumString,
        ByVal dwFlags As UInt32) As <MarshalAs(UnmanagedType.I4)> Integer 'As UCOMIEnumString
   End Interface
```

## Notes:
```cs
MyObject = new ActiveXObject("IEZoneSecurity.ZoneSecurityDemo");
```

## Notes:
```cs
<object classid="<class guid>" width=0 height=0 ID="MyObjectId" VIEWASTEXT></object>
  <script language=javascript>
    MyObject = document.getElementById("MyObjectId");
  </script>
```
