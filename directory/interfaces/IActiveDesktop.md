
## C# Definition:
```cs
[ComImport]
[Guid("F490EB00-1240-11D1-9888-006097DEACF9")]
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IActiveDesktop
{
     [PreserveSig] 
     int ApplyChanges(AD_Apply dwFlags);
     [PreserveSig] 
     int GetWallpaper([MarshalAs(UnmanagedType.LPWStr)]  System.Text.StringBuilder pwszWallpaper, 
               int cchWallpaper, 
               int dwReserved);
     [PreserveSig] 
     int SetWallpaper([MarshalAs(UnmanagedType.LPWStr)] string   pwszWallpaper, int dwReserved);
     [PreserveSig] 
     int GetWallpaperOptions(ref WALLPAPEROPT pwpo, int dwReserved);
     [PreserveSig] 
     int SetWallpaperOptions(ref WALLPAPEROPT pwpo, int dwReserved);
     [PreserveSig] 
     int GetPattern([MarshalAs(UnmanagedType.LPWStr)] System.Text.StringBuilder pwszPattern, int cchPattern, int dwReserved);
     [PreserveSig] 
     int SetPattern([MarshalAs(UnmanagedType.LPWStr)] string pwszPattern, int dwReserved);
     [PreserveSig] 
     int GetDesktopItemOptions(ref COMPONENTSOPT pco, int dwReserved);
     [PreserveSig] 
     int SetDesktopItemOptions(ref COMPONENTSOPT pco, int dwReserved);
     [PreserveSig] 
     int AddDesktopItem(ref COMPONENT pcomp, int dwReserved);
     [PreserveSig] 
     int AddDesktopItemWithUI(IntPtr hwnd, ref COMPONENT pcomp, DtiAddUI dwFlags);
     [PreserveSig] 
     int ModifyDesktopItem(ref COMPONENT pcomp, ComponentModify dwFlags);
     [PreserveSig] 
     int RemoveDesktopItem(ref COMPONENT pcomp, int dwReserved);
     [PreserveSig] 
     int GetDesktopItemCount(out int lpiCount, int dwReserved);
     [PreserveSig] 
     int GetDesktopItem(int nComponent, ref COMPONENT pcomp, int dwReserved);
     [PreserveSig] 
     int GetDesktopItemByID(IntPtr dwID, ref COMPONENT pcomp, int dwReserved);
     [PreserveSig] 
     int GenerateDesktopItemHtml([MarshalAs(UnmanagedType.LPWStr)] string pwszFileName, ref COMPONENT pcomp, int dwReserved);
     [PreserveSig] 
     int AddUrl(IntPtr hwnd, [MarshalAs(UnmanagedType.LPWStr)] string pszSource, ref COMPONENT pcomp, AddURL dwFlags);
     [PreserveSig] 
     int GetDesktopItemBySource([MarshalAs(UnmanagedType.LPWStr)] string pwszSource, ref COMPONENT pcomp, int dwReserved);
```

## VB Definition:
```cs
<ComImport(), InterfaceType(ComInterfaceType.InterfaceIsIUnknown), Guid("F490EB00-1240-11D1-9888-006097DEACF9")> _
Public Interface IActiveDesktop
    <PreserveSig()> _
    Function ApplyChanges(ByVal dwFlags As AD_Apply) As Integer
    <PreserveSig()> _
    Function GetWallpaper(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszWallpaper As StringBuilder, ByVal cchWallpaper As Integer, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function SetWallpaper(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszWallpaper As String, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GetWallpaperOptions(ByRef pwpo As WALLPAPEROPT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function SetWallpaperOptions(ByRef pwpo As WALLPAPEROPT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GetPattern(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszPattern As StringBuilder, ByVal cchPattern As Integer, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function SetPattern(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszPattern As String, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GetDesktopItemOptions(ByRef pco As COMPONENTSOPT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function SetDesktopItemOptions(ByRef pco As COMPONENTSOPT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function AddDesktopItem(ByRef pcomp As COMPONENT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function AddDesktopItemWithUI(ByVal hwnd As IntPtr, ByRef pcomp As COMPONENT, ByVal dwFlags As DtiAddUI) As Integer
    <PreserveSig()> _
    Function ModifyDesktopItem(ByRef pcomp As COMPONENT, ByVal dwFlags As ComponentModify) As Integer
    <PreserveSig()> _
    Function RemoveDesktopItem(ByRef pcomp As COMPONENT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GetDesktopItemCount(<Out()> ByRef lpiCount As Integer, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GetDesktopItem(ByVal nComponent As Integer, ByRef pcomp As COMPONENT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GetDesktopItemByID(ByVal dwID As IntPtr, ByRef pcomp As COMPONENT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function GenerateDesktopItemHtml(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszFileName As String, ByRef pcomp As COMPONENT, ByVal dwReserved As Integer) As Integer
    <PreserveSig()> _
    Function AddUrl(ByVal hwnd As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> ByVal pszSource As String, ByRef pcomp As COMPONENT, ByVal dwFlags As AddURL) As Integer
    <PreserveSig()> _
    Function GetDesktopItemBySource(<MarshalAs(UnmanagedType.LPWStr)> ByVal pwszSource As String, ByRef pcomp As COMPONENT, ByVal dwReserved As Integer) As Integer
End Interface
```

## Notes:
```cs
static readonly Guid CLSID_ActiveDesktop = new Guid("{75048700-EF1F-11D0-9888-006097DEACF9}");

public static IActiveDesktop GetActiveDesktop() 
{
     Type typeActiveDesktop = Type.GetTypeFromCLSID(CLSID_ActiveDesktop);
     return (IActiveDesktop) Activator.CreateInstance(typeActiveDesktop);
}

COMPONENTSOPT opts = new COMPONENTSOPT();
opts.dwSize = COMPONENTSOPT.SizeOf;
IActiveDesktop dt = GetActiveDesktop();
dt.GetDesktopItemOptions( ref opts, 0 );
```
