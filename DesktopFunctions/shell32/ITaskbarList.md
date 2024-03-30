
## C# Signature:
```cs
[ComImportAttribute()]
[GuidAttribute("c43dc798-95d1-4bea-9030-bb99e2983a1a")]
[InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)]
internal interface ITaskbarList4
{
     // ITaskbarList
     [PreserveSig]
     void HrInit();
     [PreserveSig]
     void AddTab(IntPtr hwnd);
     [PreserveSig]
     void DeleteTab(IntPtr hwnd);
     [PreserveSig]
     void ActivateTab(IntPtr hwnd);
     [PreserveSig]
     void SetActiveAlt(IntPtr hwnd);

     // ITaskbarList2
     [PreserveSig]
     void MarkFullscreenWindow(
     IntPtr hwnd,
     [MarshalAs(UnmanagedType.Bool)] bool fFullscreen);

     // ITaskbarList3
     [PreserveSig]
     void SetProgressValue(IntPtr hwnd, UInt64 ullCompleted, UInt64 ullTotal);
     [PreserveSig]
     void SetProgressState(IntPtr hwnd, TaskbarProgressBarStatus tbpFlags);
     [PreserveSig]
     void RegisterTab(IntPtr hwndTab, IntPtr hwndMDI);
     [PreserveSig]
     void UnregisterTab(IntPtr hwndTab);
     [PreserveSig]
     void SetTabOrder(IntPtr hwndTab, IntPtr hwndInsertBefore);
     [PreserveSig]
     void SetTabActive(IntPtr hwndTab, IntPtr hwndInsertBefore, uint dwReserved);
     [PreserveSig]
     HResult ThumbBarAddButtons(
     IntPtr hwnd,
     uint cButtons,
     [MarshalAs(UnmanagedType.LPArray)] ThumbButton[] pButtons);
     [PreserveSig]
     HResult ThumbBarUpdateButtons(
     IntPtr hwnd,
     uint cButtons,
     [MarshalAs(UnmanagedType.LPArray)] ThumbButton[] pButtons);
     [PreserveSig]
     void ThumbBarSetImageList(IntPtr hwnd, IntPtr himl);
     [PreserveSig]
     void SetOverlayIcon(
       IntPtr hwnd,
       IntPtr hIcon,
       [MarshalAs(UnmanagedType.LPWStr)] string pszDescription);
     [PreserveSig]
     void SetThumbnailTooltip(
     IntPtr hwnd,
     [MarshalAs(UnmanagedType.LPWStr)] string pszTip);
     [PreserveSig]
     void SetThumbnailClip(
     IntPtr hwnd,
     IntPtr prcClip);

     // ITaskbarList4
     void SetTabProperties(IntPtr hwndTab, SetTabPropertiesOption stpFlags);
}
```

## VB Signature:
```cs
<ComImportAttribute> _
<GuidAttribute("c43dc798-95d1-4bea-9030-bb99e2983a1a")> _
<InterfaceTypeAttribute(ComInterfaceType.InterfaceIsIUnknown)> _
Friend Interface ITaskbarList4
    ' ITaskbarList
    <PreserveSig> _
    Sub HrInit()
    <PreserveSig> _
    Sub AddTab(hwnd As IntPtr)
    <PreserveSig> _
    Sub DeleteTab(hwnd As IntPtr)
    <PreserveSig> _
    Sub ActivateTab(hwnd As IntPtr)
    <PreserveSig> _
    Sub SetActiveAlt(hwnd As IntPtr)

    ' ITaskbarList2
    <PreserveSig> _
    Sub MarkFullscreenWindow(hwnd As IntPtr, <MarshalAs(UnmanagedType.Bool)> fFullscreen As Boolean)

    ' ITaskbarList3
    <PreserveSig> _
    Sub SetProgressValue(hwnd As IntPtr, ullCompleted As UInt64, ullTotal As UInt64)
    <PreserveSig> _
    Sub SetProgressState(hwnd As IntPtr, tbpFlags As TaskbarProgressBarStatus)
    <PreserveSig> _
    Sub RegisterTab(hwndTab As IntPtr, hwndMDI As IntPtr)
    <PreserveSig> _
    Sub UnregisterTab(hwndTab As IntPtr)
    <PreserveSig> _
    Sub SetTabOrder(hwndTab As IntPtr, hwndInsertBefore As IntPtr)
    <PreserveSig> _
    Sub SetTabActive(hwndTab As IntPtr, hwndInsertBefore As IntPtr, dwReserved As UInteger)
    <PreserveSig> _
    Function ThumbBarAddButtons(hwnd As IntPtr, cButtons As UInteger, <MarshalAs(UnmanagedType.LPArray)> pButtons As ThumbButton()) As HResult
    <PreserveSig> _
    Function ThumbBarUpdateButtons(hwnd As IntPtr, cButtons As UInteger, <MarshalAs(UnmanagedType.LPArray)> pButtons As ThumbButton()) As HResult
    <PreserveSig> _
    Sub ThumbBarSetImageList(hwnd As IntPtr, himl As IntPtr)
    <PreserveSig> _
    Sub SetOverlayIcon(hwnd As IntPtr, hIcon As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> pszDescription As String)
    <PreserveSig> _
    Sub SetThumbnailTooltip(hwnd As IntPtr, <MarshalAs(UnmanagedType.LPWStr)> pszTip As String)
    <PreserveSig> _
    Sub SetThumbnailClip(hwnd As IntPtr, prcClip As IntPtr)

    ' ITaskbarList4
    Sub SetTabProperties(hwndTab As IntPtr, stpFlags As SetTabPropertiesOption)
End Interface
```
