
## C# Signatures:
```cs
[DllImport("shell32.dll", CharSet=CharSet.Auto)]
public static extern IntPtr SHGetFileInfo(string pszPath, uint dwFileAttributes, ref SHFILEINFO psfi, uint cbFileInfo, uint uFlags);
```

## VB Signature:
```cs
<DllImport("shell32.dll", CharSet:=CharSet.Auto)> _
Function SHGetFileInfo _
     (ByVal pszPath As String, _
      ByVal dwFileAttributes As Integer, _
      ByRef psfi As SHFILEINFO, _
      ByVal cbFileInfo As Integer, _
      ByVal uFlags As Integer) As IntPtr
End Function
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
public struct SHFILEINFO
{
     public IntPtr hIcon;
     public int iIcon;
     public uint dwAttributes;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 260)]
     public string szDisplayName;
     [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 80)]
     public string szTypeName;
}
```

## Sample Code:
```cs
//
    // Modified http://groups.google.com/groups?hl=en&lr=&ie=UTF-8&selm=uMD%23VHmqBHA.2368%40tkmsftngp03&rnum=4
    // 

    using System;
    using System.Runtime.InteropServices;
    using System.Drawing;

    /// <summary> Summary description for ExtractIcon.</summary>
    public class ExtractIcon
    {
    [DllImport("shell32.dll", CharSet=CharSet.Auto)]
    private static extern int  SHGetFileInfo(
      string pszPath     ,
      int    dwFileAttributes,
      out    SHFILEINFO psfi ,
      uint   cbfileInfo      ,
      SHGFI  uFlags );

    /// <summary>Maximal Length of unmanaged Windows-Path-strings</summary>
    private const int MAX_PATH = 260;
    /// <summary>Maximal Length of unmanaged Typename</summary>
    private const int MAX_TYPE = 80 ;

    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto)]
    private struct SHFILEINFO
    {
      public SHFILEINFO(bool b)
      {
        hIcon=IntPtr.Zero;
        iIcon=0;
        dwAttributes=0;
        szDisplayName="";
        szTypeName="";
      }
      public IntPtr hIcon;
      public int iIcon;
      public uint dwAttributes;
      [MarshalAs(UnmanagedType.ByValTStr, SizeConst=MAX_PATH)]
      public string szDisplayName;
      [MarshalAs(UnmanagedType.ByValTStr, SizeConst=MAX_TYPE)]
      public string szTypeName;
    };

    private ExtractIcon()
    {
    }

    [Flags]
    enum SHGFI : int
    {
      /// <summary>get icon</summary>
      Icon         = 0x000000100,   
      /// <summary>get display name</summary>
      DisplayName      = 0x000000200, 
      /// <summary>get type name</summary>
      TypeName     = 0x000000400, 
      /// <summary>get attributes</summary>
      Attributes       = 0x000000800, 
      /// <summary>get icon location</summary>
      IconLocation     = 0x000001000,  
      /// <summary>return exe type</summary>
      ExeType      = 0x000002000,  
      /// <summary>get system icon index</summary>
      SysIconIndex     = 0x000004000,  
      /// <summary>put a link overlay on icon</summary>
      LinkOverlay      = 0x000008000,  
      /// <summary>show icon in selected state</summary>
      Selected     = 0x000010000,  
      /// <summary>get only specified attributes</summary>
      Attr_Specified   = 0x000020000,  
      /// <summary>get large icon</summary>
      LargeIcon    = 0x000000000,  
      /// <summary>get small icon</summary>
      SmallIcon    = 0x000000001,  
      /// <summary>get open icon</summary>
      OpenIcon     = 0x000000002,  
      /// <summary>get shell size icon</summary>
      ShellIconSize     = 0x000000004,  
      /// <summary>pszPath is a pidl</summary>
      PIDL         = 0x000000008,  
      /// <summary>use passed dwFileAttribute</summary>
      UseFileAttributes= 0x000000010,  
      /// <summary>apply the appropriate overlays</summary>
      AddOverlays      = 0x000000020,  
      /// <summary>Get the index of the overlay in the upper 8 bits of the iIcon</summary>
      OverlayIndex     = 0x000000040,  
    }   

    /// <summary>
    /// Get the associated Icon for a file or application, this method always returns
    /// an icon.  If the strPath is invalid or there is no idonc the default icon is returned
    /// </summary>
    /// <param name="strPath">full path to the file</param>
    /// <param name="bSmall">if true, the 16x16 icon is returned otherwise the 32x32</param>
    /// <returns></returns>
    public static Icon GetIcon(string strPath, bool bSmall)
    {
        SHFILEINFO info = new SHFILEINFO(true);
        int cbFileInfo = Marshal.SizeOf(info);
        SHGFI flags;
        if (bSmall)
        flags = SHGFI.Icon|SHGFI.SmallIcon|SHGFI.UseFileAttributes;
        else
        flags = SHGFI.Icon|SHGFI.LargeIcon|SHGFI.UseFileAttributes;

        SHGetFileInfo(strPath, 256, out info,(uint)cbFileInfo, flags);
        return Icon.FromHandle(info.hIcon);
    }
    }
```

## Alternative Managed API #1:
```cs
/// <summary>
    /// Summary description for ShellIcon.  Get a small or large Icon with an easy C# function call
    /// that returns a 32x32 or 16x16 System.Drawing.Icon depending on which function you call
    /// either GetSmallIcon(string fileName) or GetLargeIcon(string fileName)
    /// </summary>
    public static class ShellIcon
    {
    [StructLayout(LayoutKind.Sequential)]
    public struct SHFILEINFO
    {
        public IntPtr hIcon;
        public IntPtr iIcon;
        public uint dwAttributes;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 260)]
        public string szDisplayName;
        [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 80)]
        public string szTypeName;
    };

    class Win32
    {
        public const uint SHGFI_ICON = 0x100;
        public const uint SHGFI_LARGEICON = 0x0; // 'Large icon
        public const uint SHGFI_SMALLICON = 0x1; // 'Small icon

        [DllImport("shell32.dll")]
        public static extern IntPtr SHGetFileInfo(string pszPath, uint dwFileAttributes, ref SHFILEINFO psfi, uint cbSizeFileInfo, uint uFlags);

        [DllImport("User32.dll")]
        public static extern int DestroyIcon(IntPtr hIcon);

    }

    static ShellIcon()
    {

    }

    public static Icon GetSmallIcon(string fileName)
    {
        return GetIcon(fileName, Win32.SHGFI_SMALLICON);
    }

    public static Icon GetLargeIcon(string fileName)
    {
        return GetIcon(fileName, Win32.SHGFI_LARGEICON);
    }

    private static Icon GetIcon(string fileName, uint flags)
    {
        SHFILEINFO shinfo = new SHFILEINFO();
        IntPtr hImgSmall = Win32.SHGetFileInfo(fileName, 0, ref shinfo, (uint)Marshal.SizeOf(shinfo), Win32.SHGFI_ICON | flags);

        Icon icon = (Icon)System.Drawing.Icon.FromHandle(shinfo.hIcon).Clone();
        Win32.DestroyIcon(shinfo.hIcon);
        return icon;
    }
    }
```
