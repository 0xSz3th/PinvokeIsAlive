
## C# Definition:
```cs
[ComImport, 
    Guid("79EAC9C1-BAF9-11CE-8C82-00AA004BA90B"), 
    InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
    public interface IBindStatusCallback
    {
        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void OnStartBinding(
            [In] uint dwReserved, 
            [In, MarshalAs(UnmanagedType.Interface)] IBinding pib);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void GetPriority(out int pnPriority);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void OnLowResource([In] uint reserved);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void OnProgress(
            [In] uint ulProgress, 
            [In] uint ulProgressMax, 
            [In] BINDSTATUS ulStatusCode, 
            [In, MarshalAs(UnmanagedType.LPWStr)] string szStatusText);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void OnStopBinding(
            [In, MarshalAs(UnmanagedType.Error)] uint hresult, 
            [In, MarshalAs(UnmanagedType.LPWStr)] string szError);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void GetBindInfo(
            out BINDF grfBINDF, 
            [In, Out] ref BINDINFO pbindinfo);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void OnDataAvailable(
            [In] uint grfBSCF, 
            [In] uint dwSize, 
            [In] ref FORMATETC pFormatetc, 
            [In] ref STGMEDIUM pStgmed);

        [MethodImpl(MethodImplOptions.InternalCall, 
        MethodCodeType=MethodCodeType.Runtime)]
        void OnObjectAvailable(
            [In] ref Guid riid, 
            [In, MarshalAs(UnmanagedType.IUnknown)] object punk);
    }
```

## VB Definition:
```cs
TODO
```

## User-Defined Types:
```cs
[Flags]
    public enum BINDVERB : uint
    {
        BINDVERB_GET       = 0x00000000,       // default action
        BINDVERB_POST      = 0x00000001,       // post verb
        BINDVERB_PUT       = 0x00000002,       // put verb
        BINDVERB_CUSTOM    = 0x00000003,       // custom verb
    } 

    // flags that describe the type of transaction that caller wants
    [Flags]
    public enum BINDF : uint
        {
     BINDF_DEFAULT             = 0x00000000
    ,BINDF_ASYNCHRONOUS          = 0x00000001
    ,BINDF_ASYNCSTORAGE          = 0x00000002
    ,BINDF_NOPROGRESSIVERENDERING    = 0x00000004
    ,BINDF_OFFLINEOPERATION      = 0x00000008
    ,BINDF_GETNEWESTVERSION      = 0x00000010
    ,BINDF_NOWRITECACHE          = 0x00000020
    ,BINDF_NEEDFILE          = 0x00000040
    ,BINDF_PULLDATA          = 0x00000080
    ,BINDF_IGNORESECURITYPROBLEM     = 0x00000100
    ,BINDF_RESYNCHRONIZE         = 0x00000200
    ,BINDF_HYPERLINK         = 0x00000400
    ,BINDF_NO_UI             = 0x00000800
    ,BINDF_SILENTOPERATION       = 0x00001000
    ,BINDF_PRAGMA_NO_CACHE       = 0x00002000

    ,BINDF_GETCLASSOBJECT        = 0x00004000
    ,BINDF_RESERVED_1        = 0x00008000

    // bindstatus callback from client is free threaded
    ,BINDF_FREE_THREADED         = 0x00010000
    // client does not need to know excat size of data available
    // hence the read goes directly to e.g. socket
    ,BINDF_DIRECT_READ           = 0x00020000
    // is the transaction a forms submit.
    ,BINDF_FORMS_SUBMIT          = 0x00040000
    ,BINDF_GETFROMCACHE_IF_NET_FAIL  = 0x00080000
    // binding is from UrlMoniker
    ,BINDF_FROMURLMON        = 0x00100000
    ,BINDF_FWD_BACK          = 0x00200000

    ,BINDF_PREFERDEFAULTHANDLER      = 0x00400000
    ,BINDF_ENFORCERESTRICTED     = 0x00800000

    // Note:
    // the highest byte 0x??000000 is used internally
    // see other documentation
    }
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto, Pack=4)]
    public struct SECURITY_ATTRIBUTES
    {
        public uint nLength;
        public uint lpSecurityDescriptor;
        public int bInheritHandle;
    }

    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto, Pack=4)]
    public struct BINDINFO
    {
        public uint cbSize;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string szExtraInfo;
        public STGMEDIUM stgmedData;
        public uint grfBindInfoF;
        public BINDVERB dwBindVerb;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string szCustomVerb;
        public uint cbstgmedData;
        public uint dwOptions;
        public uint dwOptionsFlags;
        public uint dwCodePage;
        public SECURITY_ATTRIBUTES securityAttributes;
        public Guid iid;
        [MarshalAs(UnmanagedType.IUnknown)]
        public object punk;
        public uint dwReserved;
    }

    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto, Pack=4), ComConversionLoss]
    public struct FORMATETC
    {
        public uint cfFormat;
        [ComConversionLoss]
        public IntPtr ptd;
        public uint dwAspect;
        public int lindex;
        public uint tymed;
    }

    [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Auto, Pack=4), ComConversionLoss]
    public struct STGMEDIUM
    {
        public uint tymed;
        [ComConversionLoss]
        public IntPtr data;
        [MarshalAs(UnmanagedType.IUnknown)]
        public object pUnkForRelease;
    }
```

## User-Defined Types:
```cs
public enum BINDSTATUS : uint
    {
     BINDSTATUS_FINDINGRESOURCE      = 1
    ,BINDSTATUS_CONNECTING
    ,BINDSTATUS_REDIRECTING
    ,BINDSTATUS_BEGINDOWNLOADDATA
    ,BINDSTATUS_DOWNLOADINGDATA
    ,BINDSTATUS_ENDDOWNLOADDATA
    ,BINDSTATUS_BEGINDOWNLOADCOMPONENTS
    ,BINDSTATUS_INSTALLINGCOMPONENTS
    ,BINDSTATUS_ENDDOWNLOADCOMPONENTS
    ,BINDSTATUS_USINGCACHEDCOPY
    ,BINDSTATUS_SENDINGREQUEST
    ,BINDSTATUS_CLASSIDAVAILABLE
    ,BINDSTATUS_MIMETYPEAVAILABLE
    ,BINDSTATUS_CACHEFILENAMEAVAILABLE
    ,BINDSTATUS_BEGINSYNCOPERATION
    ,BINDSTATUS_ENDSYNCOPERATION
    ,BINDSTATUS_BEGINUPLOADDATA
    ,BINDSTATUS_UPLOADINGDATA
    ,BINDSTATUS_ENDUPLOADDATA
    ,BINDSTATUS_PROTOCOLCLASSID
    ,BINDSTATUS_ENCODING
    ,BINDSTATUS_VERIFIEDMIMETYPEAVAILABLE
    ,BINDSTATUS_CLASSINSTALLLOCATION
    ,BINDSTATUS_DECODING
    ,BINDSTATUS_LOADINGMIMEHANDLER
    ,BINDSTATUS_CONTENTDISPOSITIONATTACH
    ,BINDSTATUS_FILTERREPORTMIMETYPE
    ,BINDSTATUS_CLSIDCANINSTANTIATE
    ,BINDSTATUS_IUNKNOWNAVAILABLE
    ,BINDSTATUS_DIRECTBIND
    ,BINDSTATUS_RAWMIMETYPE
    ,BINDSTATUS_PROXYDETECTING
    ,BINDSTATUS_ACCEPTRANGES
    ,BINDSTATUS_COOKIE_SENT
    ,BINDSTATUS_COMPACT_POLICY_RECEIVED
    ,BINDSTATUS_COOKIE_SUPPRESSED
    ,BINDSTATUS_COOKIE_STATE_UNKNOWN
    ,BINDSTATUS_COOKIE_STATE_ACCEPT
    ,BINDSTATUS_COOKIE_STATE_REJECT
    ,BINDSTATUS_COOKIE_STATE_PROMPT
    ,BINDSTATUS_COOKIE_STATE_LEASH
    ,BINDSTATUS_COOKIE_STATE_DOWNGRADE
    ,BINDSTATUS_POLICY_HREF
    ,BINDSTATUS_P3P_HEADER
    ,BINDSTATUS_SESSION_COOKIE_RECEIVED
    ,BINDSTATUS_PERSISTENT_COOKIE_RECEIVED
    ,BINDSTATUS_SESSION_COOKIES_ALLOWED
    }
```

## Sample:
```cs
using System;
using System.Runtime.InteropServices;
using System.Runtime.CompilerServices;
using System.IO;
using System.ComponentModel;
using System.Threading;

namespace DownloaderDotNet
{
    public enum HRESULTS :long
    {
        S_OK = 0,
        S_FALSE = 1,

        E_NOTIMPL = 0x80004001,
        E_OUTOFMEMORY = 0x8007000E,
        E_INVALIDARG = 0x80070057,
        E_NOINTERFACE = 0x80004002,
        E_POINTER = 0x80004003,
        E_HANDLE = 0x80070006,
        E_ABORT = 0x80004004,
        E_FAIL = 0x80004005,
        E_ACCESSDENIED = 0x80070005,

        // IConnectionPoint errors

        CONNECT_E_FIRST = 0x80040200,
        CONNECT_E_NOCONNECTION,  // there is no connection for this connection id
        CONNECT_E_ADVISELIMIT,   // this implementation's limit for advisory connections has been reached
        CONNECT_E_CANNOTCONNECT, // connection attempt failed
        CONNECT_E_OVERRIDDEN,    // must use a derived interface to connect

        // DllRegisterServer/DllUnregisterServer errors
        SELFREG_E_TYPELIB = 0x80040200, // failed to register/unregister type library
        SELFREG_E_CLASS,        // failed to register/unregister class

        // INET errors

        INET_E_INVALID_URL = 0x800C0002,
        INET_E_NO_SESSION = 0x800C0003,
        INET_E_CANNOT_CONNECT = 0x800C0004,
        INET_E_RESOURCE_NOT_FOUND = 0x800C0005,
        INET_E_OBJECT_NOT_FOUND = 0x800C0006,
        INET_E_DATA_NOT_AVAILABLE = 0x800C0007,
        INET_E_DOWNLOAD_FAILURE = 0x800C0008,
        INET_E_AUTHENTICATION_REQUIRED = 0x800C0009,
        INET_E_NO_VALID_MEDIA = 0x800C000A,
        INET_E_CONNECTION_TIMEOUT = 0x800C000B,
        INET_E_INVALID_REQUEST = 0x800C000C,
        INET_E_UNKNOWN_PROTOCOL = 0x800C000D,
        INET_E_SECURITY_PROBLEM = 0x800C000E,
        INET_E_CANNOT_LOAD_DATA = 0x800C000F,
        INET_E_CANNOT_INSTANTIATE_OBJECT = 0x800C0010,
        INET_E_USE_DEFAULT_PROTOCOLHANDLER = 0x800C0011,
        INET_E_DEFAULT_ACTION = 0x800C0011,
        INET_E_USE_DEFAULT_SETTING = 0x800C0012,
        INET_E_QUERYOPTION_UNKNOWN = 0x800C0013,
        INET_E_REDIRECT_FAILED = 0x800C0014,//INET_E_REDIRECTING 
        INET_E_REDIRECT_TO_DIR = 0x800C0015,
        INET_E_CANNOT_LOCK_REQUEST = 0x800C0016,
        INET_E_USE_EXTEND_BINDING = 0x800C0017,
        INET_E_ERROR_FIRST = 0x800C0002,
        INET_E_ERROR_LAST = 0x800C0017,
        INET_E_CODE_DOWNLOAD_DECLINED = 0x800C0100,
        INET_E_RESULT_DISPATCHED = 0x800C0200,
        INET_E_CANNOT_REPLACE_SFP_FILE = 0x800C0300,

    }
    /// <summary>
    /// file downloader class
    /// </summary>
    [ClassInterface(ClassInterfaceType.None)]
    public class Downloader : IBindStatusCallback,IDisposable

    {
        public Downloader()
        {
            // 
            // TODO: Add constructor logic here
            //
        }
        public delegate void DownloadEvent(string file);
        public delegate void DownloadAborted(string file,long Errorcode,string Message);
        public delegate void DownloadProgress(string file,long ReceivedBytes,long TotalBytes);
        public event DownloadEvent  OnDownloadStarted;
        public event DownloadEvent  OnDownloadComplete;
        public event DownloadAborted  OnDownloadAborted;
        public event DownloadProgress  OnDownloadProgress;

        private  IBinding mobjBinding;
        private bool IsAborted=false;
        public string LocalPath;
        public string SourcePath;
```

## Sample:
```cs
#region IDisposable Members
        //finalizer
        ~Downloader()
        {
            Dispose(false);
        }
        //disposer
        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        //dispose
        bool disposed=false;
        /// <summary>
        /// Dispose and free used resources
        /// </summary>
        protected virtual void Dispose(bool disposing)
        {
            if(disposing )
            {
                if(!disposed)
                {
                    StopDownload();
                    if(mobjBinding!=null)
                    Marshal.ReleaseComObject(mobjBinding);
                    mobjBinding=null;
                    disposed=true;
                }
            }
        }
        #endregion

        /// <summary>
        /// The URLMON library contains this function, URLDownloadToFile, which is a way
        /// to download files without user prompts. 
        /// </summary>
        /// <param name="pCaller">Pointer to caller object (AX).</param>
        /// <param name="szURL">String of the URL.</param>
        /// <param name="szFileName">String of the destination filename/path.</param>
        /// <param name="dwReserved">[reserved].</param>
        /// <param name="lpfnCB">A callback function to monitor progress or abort.</param>
        /// <returns>throws exception if not success</returns>
        [DllImport("urlmon.dll", CharSet=CharSet.Auto,SetLastError=true, PreserveSig=false)]
        public static extern void URLDownloadToFile(
            [MarshalAs(UnmanagedType.IUnknown)] object pAxCaller,
            [MarshalAs(UnmanagedType.LPWStr)] string szURL,
            [MarshalAs(UnmanagedType.LPWStr)] string szFileName,
            [MarshalAs(UnmanagedType.U4)] uint dwReserved,
            [MarshalAs(UnmanagedType.Interface)] IBindStatusCallback lpfnCB);
```

## Sample:
```cs
public void Download()
        {
            try
            {
                IsAborted=false;
                if( mobjBinding ==null)
                {
                    string destdir=Path.GetDirectoryName(this.LocalPath);
                    if(!Directory.Exists(destdir))
                        Directory.CreateDirectory(destdir);
                    URLDownloadToFile(IntPtr.Zero, SourcePath , LocalPath ,0,(IBindStatusCallback)this);//use 0x10 for new download

                }
            }
            catch(Exception e)
            {
                Win32Exception we=new Win32Exception(Marshal.GetLastWin32Error() ,e.Message);

                 //System.Windows.Forms.MessageBox.Show("Download error: \r\n"+we.Message);
            }
        }

        public void StopDownload()
        {
            try
            {
                if(mobjBinding!=null)
                lock(mobjBinding)
                {
                    if(mobjBinding!=null)
                        mobjBinding.Abort();
                    IsAborted=true;
                }
            }
            catch(Exception ex)
            {
                System.Windows.Forms.MessageBox.Show("Download error: \r\n"+ex.Message);

            }
        }

        public void GetBindInfo(out BINDF grfBINDF ,ref BINDINFO pbindinfo )
        {
            grfBINDF=BINDF.BINDF_IGNORESECURITYPROBLEM;
            try
            {
                uint cbSize = pbindinfo.cbSize;        // remember incoming cbSize
                pbindinfo=new BINDINFO();//reset
                pbindinfo.cbSize = cbSize;                // restore cbSize
                pbindinfo.dwBindVerb = BINDVERB.BINDVERB_GET;    // set verb
                pbindinfo.stgmedData.tymed=0;
                pbindinfo.cbstgmedData=(uint)Marshal.SizeOf(pbindinfo.stgmedData);
                pbindinfo.dwOptions=0;
                pbindinfo.dwOptionsFlags=0;
                pbindinfo.dwReserved=0;
            }
            catch(Exception ex)
            {
                System.Windows.Forms.MessageBox.Show("Download error: \r\n"+ex.Message);

            }
        }
        public void GetPriority(out int pnPriority)
        {
            pnPriority=0;  //THREAD_PRIORITY_NORMAL=0,THREAD_PRIORITY_BELOW_NORMAL=-1
        }
        public void  OnDataAvailable( uint grfBSCF , uint dwSize ,ref FORMATETC pformatetc ,ref STGMEDIUM pstgmed )
        {
        }
        public void OnLowResource( uint reserved )
        {
        }
        public void OnObjectAvailable(ref Guid riid , object punk )
        {
        }
        public void OnProgress(uint ulProgress , uint ulProgressMax , BINDSTATUS ulStatusCode ,string szStatusText )
        {
             if( ulProgressMax > 0)
                 if(OnDownloadProgress!=null)
                    OnDownloadProgress(SourcePath,ulProgress, ulProgressMax);
            if(mobjBinding!=null && IsAborted)
                mobjBinding.Abort();
        }
        public void OnStartBinding (uint dwReserved , IBinding pib )
        {
            IsAborted=false;
            mobjBinding = pib;
            if(OnDownloadStarted!=null)
                OnDownloadStarted(SourcePath);
        }
        public void OnStopBinding (uint hresult , string szError )
        {
            try
            {
                if( hresult == 1)
                {
                    if(OnDownloadComplete!=null)
                        OnDownloadComplete(SourcePath);
                }
                else
                {
                    if(OnDownloadAborted!=null)
                        OnDownloadAborted(SourcePath,hresult, ErrorDescription(hresult));
                }
            }
            catch(Exception ex)
            {
                System.Windows.Forms.MessageBox.Show("Download error: \r\n"+ex.Message);
            }
             mobjBinding = null;
        }

        private string ErrorDescription(long ErrNum )
        {
            string Description="";

            switch((HRESULTS)ErrNum)
            {
                case HRESULTS.INET_E_AUTHENTICATION_REQUIRED:
                    Description = "Authentication Failure.";
                    break;
                case HRESULTS.INET_E_CANNOT_CONNECT:
                    Description = "Cannot Connect";break;
                case HRESULTS.INET_E_CANNOT_INSTANTIATE_OBJECT:
                    Description = "Cannot Instantiate Object.";break;
                case HRESULTS.INET_E_CANNOT_LOAD_DATA:
                    Description = "Cannot Load Data.";break;
                case HRESULTS.INET_E_CANNOT_LOCK_REQUEST:
                    Description = "Cannot Lock Request.";break;
                case HRESULTS.INET_E_CANNOT_REPLACE_SFP_FILE:
                    Description = "Cannot Replace SFP File.";break;
                case HRESULTS.INET_E_CODE_DOWNLOAD_DECLINED:
                    Description = "Code Download Declined.";break;
                case HRESULTS.INET_E_CONNECTION_TIMEOUT:
                    Description = "Connection Timeout.";break;
                case HRESULTS.INET_E_DATA_NOT_AVAILABLE:
                    Description = "Data Not Available.";break;
                case HRESULTS.INET_E_DEFAULT_ACTION:
                    Description = "Default Action.";break;
                case HRESULTS.INET_E_DOWNLOAD_FAILURE:
                    Description = "Download Failure.";break;
                case HRESULTS.INET_E_INVALID_REQUEST:
                    Description = "Invalid Request.";break;
                case HRESULTS.INET_E_INVALID_URL:
                    Description = "Invalid URL.";break;
                case HRESULTS.INET_E_NO_SESSION:
                    Description = "No Session.";break;
                case HRESULTS.INET_E_NO_VALID_MEDIA:
                    Description = "No Valid Media.";break;
                case HRESULTS.INET_E_OBJECT_NOT_FOUND:
                    Description = "File Not Found.";break;
                case HRESULTS.INET_E_QUERYOPTION_UNKNOWN:
                    Description = "QueryOption Unknown.";break;
                case HRESULTS.INET_E_REDIRECT_FAILED:
                    Description = "Redirect Failed.";break;
                case HRESULTS.INET_E_REDIRECT_TO_DIR:
                    Description = "Redirect To Dir.";break;
                case HRESULTS.INET_E_RESOURCE_NOT_FOUND:
                    Description = "Resource Not Found.";break;
                case HRESULTS.INET_E_RESULT_DISPATCHED:
                    Description = "Result Dispatched.";break;
                case HRESULTS.INET_E_SECURITY_PROBLEM:
                    Description = "Security Problem.";break;
                case HRESULTS.INET_E_UNKNOWN_PROTOCOL:
                    Description = "Unknown Protocol.";break;
                default:
                    Description = "Unknown Error.";break;
            }
            if(IsAborted)
                Description = "Download aborted.";
            return Description;
        }

    }

    //implementation
    public class MyDownload
    {
        public MyDownload()
        {
        }

        public void DownloadFile(string LocalPath,string RemotePath)
        {
            Downloader  downloader=new Downloader();
            downloader.LocalPath=LocalPath;
            downloader.SourcePath=RemotePath;
            downloader.OnDownloadStarted+=new Downloader.DownloadEvent(downloader_OnDownloadStarted);
            downloader.OnDownloadProgress+=new Downloader.DownloadProgress(downloader_OnDownloadProgress);
            downloader.OnDownloadAborted+=new Downloader.DownloadAborted(downloader_OnDownloadAborted);
            downloader.OnDownloadComplete+=new Downloader.DownloadEvent(downloader_OnDownloadComplete);

            downloader.Download();
            downloader.Dispose();
            downloader=null;
        }
        public static void downloader_OnDownloadStarted(string file)
        {
            //todo:custom implementations
        }
        public static void downloader_OnDownloadComplete(string file)
        {//todo:custom implementations
        }
        private void downloader_OnDownloadProgress(string file, long ReceivedBytes, long TotalBytes)
        {//todo:custom implementations
        }
        private void downloader_OnDownloadAborted(string file, long Errorcode, string Message)
        {//todo:custom implementations
        }

    }
```
