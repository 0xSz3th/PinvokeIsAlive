
## C# Signature:
```cs
[DllImport("shell32.dll", ExactSpelling=true, PreserveSig=false)]
static extern void SHBindToParent(
    [In, MarshalAs(UnmanagedType.LPStruct)] ITEMIDLIST pidl, 
    [In, MarshalAs(UnmanagedType.LPStruct)] Guid riid,
    [MarshalAs(UnmanagedType.Interface)] out object ppv, 
    IntPtr ppidlLast);
```

## VB Signature:
```cs
<DllImport("shell32")> _
    Function SHBindToParent( _
    ByVal lpifq As IntPtr, _
    ByRef riid As Guid, _
    ByRef ppv As IntPtr, _
    ByRef pidlLast As IntPtr) As Integer
    End Function
```

## VB Signature:
```cs
Declare Auto Function SHBindToParent Lib "shell32.dll" ( _
    ByVal pidl As IntPtr, _
    <[In](), MarshalAs(UnmanagedType.LPStruct)> ByVal riid As Guid, _
    ByRef ppv As IntPtr, _
    ByRef ppidlLast As IntPtr) As Integer
```

## C# Signature:
```cs
[DllImport("shell32")]
        public static extern int SHBindToParent (
            IntPtr lpifq,
            [In] ref Guid riid,
            /* interface whose IID is riid */ out IntPtr ppv,
            out IntPtr pidlLast );
```

## Sample Code:
```cs
public class ShellFunctions
    {

    [DllImport("shlwapi")]
    public static extern Int32 StrRetToBuf(
        ref STRRET pstr,
        IntPtr pidl,
        StringBuilder pszBuf,
        uint cchBuf );

    public static IntPtr NextPIDL(
                     IntPtr myIntPtr)
    {
        short cb = Marshal.ReadInt16(myIntPtr);

        return new IntPtr((int)myIntPtr + cb);
        // must have 'int' here
        // it changes the IntPtr myIntPtr
        // to 'int', a memory address
    }
    //---------------------------------

    private static int GetPIDLCount(
                      IntPtr IDList)
    {
        int Result = 0;
        if (IDList != IntPtr.Zero)
        {
        short cb = Marshal.ReadInt16(IDList);
        while (cb != 0)
        {
            Result++;
            IDList = NextPIDL(IDList);
            cb = Marshal.ReadInt16(IDList);
        }
        }
        return Result;
    }
    //---------------------------------

    public static string
        GetDisplayName (
                IShellFolder ShellFolder,
                IntPtr ppidl,
                bool ForParsing )
    {
        string MyComputer = string.Empty;
        if ( GetPIDLCount( ppidl ) > 1 )
        MessageBox.Show ( "GetDisplayName(), PIDL count > 1" );

        ESHGDN Flags = ForParsing ?
        ESHGDN.SHGDN_FORPARSING :
        ESHGDN.SHGDN_NORMAL;
            try
            {
                STRRET   strret = new STRRET();
                ShellFolder.GetDisplayNameOf(
                    ppidl,
                    Flags ,
                    out strret );
                StringBuilder sb = new StringBuilder( 260 );
                StrRetToBuf ( 
                    ref strret,
                    ppidl,
                    sb,
                    260 );
                MyComputer = sb.ToString();
            }
            catch {}
            return MyComputer;  // must test for string.Empty

    }

    public static 
    string GetParsableDisplayName ( IntPtr lpifq )  
    {
        IntPtr lpi;
        IntPtr SfParent;

        SHBindToParent ( 
            lpifq,
            ref Guid_IShellFolder.IID_IShellFolder,
            out SfParent,
            out lpi );

        Object obj = Marshal.GetObjectForIUnknown( SfParent );
        IShellFolder sfParent = obj as IShellFolder;

        string parsableName =
                GetDisplayName (
                    sfParent,
                    lpi,
                    true );        
        return parsableName;
    }
    //---------------------------------
```

## Sample Code:
```cs
/// <summary>
    ///  managed equivalent of IShellFolder interface
    /// </summary>
    [ComImport]
    [InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    [Guid("000214E6-0000-0000-C000-000000000046")]
    public interface IShellFolder 
    {
    void ParseDisplayName( 
        IntPtr hwnd,
        IntPtr pbc,    
        String pszDisplayName,
        UInt32 pchEaten,
        out IntPtr ppidl,    
        UInt32 pdwAttributes);    

    void EnumObjects( 
        IntPtr hwnd,
        ESHCONTF grfFlags,
        out IntPtr ppenumIDList);    

    void BindToObject( 
        IntPtr pidl,        
        IntPtr pbc,        
        [In] ref Guid riid,        
        out IntPtr ppv);    

    void BindToStorage( 
        IntPtr pidl,
        IntPtr pbc,    
        [In] ref Guid riid,        
        out IntPtr ppv);    

    [PreserveSig]
        Int32 CompareIDs( 
        Int32 lParam,    
        IntPtr pidl1,    
        IntPtr pidl2);    

    void CreateViewObject( 
        IntPtr hwndOwner,    
        [In] ref Guid riid,        
        out IntPtr ppv);    

    /*    this version is good if cidl is one
 *    void GetAttributesOf( 
            UInt32 cidl,
            ref IntPtr apidl,
            ref ESFGAO rgfInOut);
   */
```

## Sample Code:
```cs
void GetAttributesOf( 
        UInt32 cidl,
        [MarshalAs(UnmanagedType.LPArray, SizeParamIndex=0)]
        IntPtr[] apidl,
        ref ESFGAO rgfInOut);

    void GetUIObjectOf( 
        IntPtr hwndOwner,
        UInt32 cidl,    // number of IntPtr's in incoming array
        [MarshalAs(UnmanagedType.LPArray, SizeParamIndex=1)]
        IntPtr[] apidl,
        [In] ref Guid riid,
        UInt32 rgfReserved,
        out IntPtr ppv);

    /*    this version is good if cidl is one
          void GetUIObjectOf(
          IntPtr hwndOwner,
          UInt32 cidl,
          ref    IntPtr apidl,
          [In] ref Guid riid,
          UInt32 rgfReserved,
          out IntPtr ppv);
       */
    void GetDisplayNameOf(
        IntPtr pidl,
        ESHGDN uFlags,
        out STRRET pName);

    void SetNameOf( 
        IntPtr hwnd,    
        IntPtr pidl,    
        String pszName,    
        ESHCONTF uFlags,    
        out IntPtr ppidlOut);    
    }

    // from ShObjIdl.h
    public enum ESFGAO : uint
    {
    SFGAO_CANCOPY     =  0x00000001,
    SFGAO_CANMOVE     =  0x00000002,
    SFGAO_CANLINK     =  0x00000004,
    SFGAO_LINK        =  0x00010000,
    SFGAO_SHARE       =  0x00020000,
    SFGAO_READONLY    =  0x00040000,
    SFGAO_HIDDEN      =  0x00080000,
    SFGAO_FOLDER      =  0x20000000,
    SFGAO_FILESYSTEM      =  0x40000000,
    SFGAO_HASSUBFOLDER    =  0x80000000,
    }

    public enum ESHCONTF
    {
    SHCONTF_FOLDERS = 0x0020,
    SHCONTF_NONFOLDERS = 0x0040,
    SHCONTF_INCLUDEHIDDEN = 0x0080,
    SHCONTF_INIT_ON_FIRST_NEXT = 0x0100,
    SHCONTF_NETPRINTERSRCH  = 0x0200,
    SHCONTF_SHAREABLE = 0x0400,
    SHCONTF_STORAGE = 0x0800   
    }
      // from shlobj.h
    public enum ESHGDN 
    {
    SHGDN_NORMAL             = 0x0000,
    SHGDN_INFOLDER           = 0x0001,
    SHGDN_FOREDITING         = 0x1000,
    SHGDN_FORADDRESSBAR     = 0x4000,
    SHGDN_FORPARSING        = 0x8000,
    }

    public  enum ESTRRET : int
    {
    eeRRET_WSTR     = 0x0000,            // Use STRRET.pOleStr
    STRRET_OFFSET   = 0x0001,    // Use STRRET.uOffset to Ansi
    STRRET_CSTR     = 0x0002            // Use STRRET.cStr
    }

    /*
    // Microsoft's sample and it works too.
    //    see sample,    Unions.cs

    union MYUNION2
    {
    int i;
    char str[128];
    };
```

## Sample Code:
```cs
[ StructLayout( LayoutKind.Explicit, Size=128 )]
    public struct MyUnion2_1
    {
    [ FieldOffset( 0 )]
    public int i;
    }
    */
    // shlobj.h

    // this works too...from Unions.cs
    [StructLayout(LayoutKind.Explicit, Size=520)]
    public struct STRRETinternal
    {
    [FieldOffset(0)]
    public IntPtr pOleStr;

    [FieldOffset(0)]
    public IntPtr pStr;  // LPSTR pStr;   NOT USED

    [FieldOffset(0)]
    public uint  uOffset;

    }

    [StructLayout(LayoutKind.Sequential )]
    public struct STRRET
    {
    public uint uType;
    public STRRETinternal data;
    }

    public class Guid_IShellFolder 
    {
    public static Guid IID_IShellFolder =
        new Guid("{000214E6-0000-0000-C000-000000000046}");
    }
```
