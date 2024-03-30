
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern IntPtr CreateMutex(IntPtr lpMutexAttributes, bool bInitialOwner,
   string lpName);
```

## VB.Net Signature:
```cs
<DllImport("Kernel32.dll", CharSet:=CharSet.Auto, setlasterror:=True)> _
    Public Function CreateMutex(ByVal lpMutexAttributes As IntPtr, _
    ByVal bInitialOwner As Boolean, _
    ByVal lpName As String) As IntPtr
    End Function
```

## Sample Code:
```cs
//// Win32Calls.cs ////////////////////////////
namespace nsWin32Calls
{
    /// <summary>
    /// Win32 calls encapsulation object.
    /// </summary>
    public class Win32Calls
    {
        ...
        [DllImport("kernel32.dll", SetLastError = true)]
        public static extern IntPtr CreateMutex( IntPtr lpMutexAttributes, 
            bool bInitialOwner, string lpName );

        [DllImport("kernel32.dll")]
        public static extern bool ReleaseMutex( IntPtr hMutex );
        ...
        /// <summary>
        /// This value can be returned by CreateMutex() and is found in
        /// C++ in the error.h header file.
        /// </summary>
        public const int    ERROR_ALREADY_EXISTS    = 183;
        ...
    }
}

//// frmMain.cs ///////////////////////////////

...
using nsWin32Calls;        // encapsulates Win32 calls
...

namespace dsh
{
    public class frmMain : System.Windows.Forms.Form
    {
        ...
        // helper objects
        private static frmMain        form = null;
        ...
        /// <summary>
        /// Main entry point for the application.
        /// </summary>
        [STAThread]
        public static void Main()
        {
            // create IntPtrs for use with CreateMutex()
            IntPtr    ipMutexAttr = new IntPtr( 0 );
            IntPtr    ipHMutex = new IntPtr( 0 );

            try 
            {
                // Create the mutex and verify its status BEFORE construction
                // of the main form.

                ipHMutex = Win32Calls.CreateMutex( ipMutexAttr, 
                    true, "CompanyName_AppName_MUTEX" );

                if (ipHMutex != IntPtr.Zero)
                {
                    // check GetLastError value (MUST use this call. See MSDN)

                    int iGLE = Marshal.GetLastWin32Error();

                    // if we get the ERROR_ALREADY_EXISTS value, there is 
                    // already another instance of this application running.

                    if (iGLE == Win32Calls.ERROR_ALREADY_EXISTS)
                        // So, don't allow this instance to run.
                        return;
                }
                else    
                {    // CreateMutex() failed.
                    // once the app is up and running, I log the failure from
                    // within the frmMain constructor.
                    m_bMutexFailed = true;
                }

                // construct the main form object and
                form = new frmMain();

                // run the app.
                Application.Run( form );

            }
            catch( Exception oEx )
            {
                ...handle it...
            }
            finally
            {
                // release the mutex
                if (ipHMutex != (IntPtr)0)
                    Win32Calls.ReleaseMutex( ipHMutex );

                // cleanup the main form object instance.
                if (form != null) {
                    form.Dispose();
                }
            }
        }
        ...
    }
}
```

## Another Sample implementation
```cs
/// <summary>
    /// Summary description for Native.
    /// </summary>
    internal sealed class Native
    {
        /// <summary>
        /// This value can be returned by CreateMutex() and is found in
        /// C++ in the error.h header file.
        /// </summary>
        public const int    ERROR_ALREADY_EXISTS    = 183;
        public const uint SYNCHRONIZE         = 0x00100000;

        [DllImport("kernel32.dll")]
        public static extern IntPtr CreateMutex(IntPtr lpMutexAttributes, bool bInitialOwner, string lpName);

        [DllImport("kernel32.dll")]
        public static extern bool ReleaseMutex( IntPtr hMutex );

        [DllImport("kernel32.dll")]
        public static extern IntPtr OpenMutex(uint dwDesiredAccess, bool bInheritHandle, string lpName);

        [DllImport("advapi32.dll", SetLastError=true)]
        public static extern bool SetSecurityDescriptorDacl(ref SECURITY_DESCRIPTOR securityDescriptor, bool daclPresent, IntPtr dacl, bool daclDefaulted);

        [DllImport("advapi32.dll", SetLastError=true)]
        public static extern bool InitializeSecurityDescriptor(out SECURITY_DESCRIPTOR securityDescriptor, uint dwRevision);

        [StructLayoutAttribute(LayoutKind.Sequential)]
        public struct SECURITY_DESCRIPTOR 
        {
            public byte revision;
            public byte size;
            public short control;
            public IntPtr owner;
            public IntPtr group;
            public IntPtr sacl;
            public IntPtr dacl;
        }

        [StructLayout(LayoutKind.Sequential)]
        public struct SECURITY_ATTRIBUTES
        {
            public int nLength;
            public IntPtr lpSecurityDescriptor;
            public int bInheritHandle;
        }

        /// <summary>
        /// Security enumeration from:
        /// http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dllproc/base/synchronization_object_security_and_access_rights.asp
        /// </summary>
        [Flags]
        public enum SyncObjectAccess : uint
        {
            DELETE            = 0x00010000,
            READ_CONTROL        = 0x00020000,
            WRITE_DAC        = 0x00040000,
            WRITE_OWNER        = 0x00080000,
            SYNCHRONIZE        = 0x00100000,
            EVENT_ALL_ACCESS    = 0x001F0003,
            EVENT_MODIFY_STATE    = 0x00000002,
            MUTEX_ALL_ACCESS    = 0x001F0001,
            MUTEX_MODIFY_STATE    = 0x00000001,
            SEMAPHORE_ALL_ACCESS    = 0x001F0003,
            SEMAPHORE_MODIFY_STATE    = 0x00000002,
            TIMER_ALL_ACCESS    = 0x001F0003,
            TIMER_MODIFY_STATE    = 0x00000002,
            TIMER_QUERY_STATE    = 0x00000001
        }
    }
```

## Another Sample implementation
```cs
public class SecurityNeutralMutex
    {
        [ Serializable ]
        public class MutexCreationException : ApplicationException
        {
            public MutexCreationException( string msg ) : base( msg )
            {
            }

            public MutexCreationException( string msg, Exception ex ) : base( msg, ex )
            {
            }

            public MutexCreationException( SerializationInfo info, StreamingContext context ) : base( info, context )
            {
            }
        }

        public SecurityNeutralMutex()
        {
        }

        public static Mutex CeateMutex( bool initiallyOwned, string name, out bool createdNew )
        {
            Mutex mutex = new Mutex( false ) ;
            mutex.Close();
            mutex.Handle = InternalCreateMutex( initiallyOwned, name, out createdNew );

            return mutex;
        }

        private static IntPtr InternalCreateMutex( bool initiallyOwned, string name, out bool createdNew )
        {

            IntPtr mutexAttributesPtr = new IntPtr( 0 );
            IntPtr securityDescPtr = new IntPtr( 0 );
            bool worked;
            const uint SdRevisionLevel = 1;
            try
            {
                int lastError = 0;
                // It's faster to first try OpenMutex
                IntPtr hMutex = Native.OpenMutex( ( uint ) ( Native.SyncObjectAccess.MUTEX_MODIFY_STATE ), false, name );
                createdNew = false;
                if ( hMutex == IntPtr.Zero )
                {
                    // Initialize the security descriptor structure
                    Native.SECURITY_DESCRIPTOR securityDesc;
                    worked = Native.InitializeSecurityDescriptor( out securityDesc, SdRevisionLevel );
                    if( ! worked )
                    {
                        lastError = Marshal.GetLastWin32Error();
                        throw new MutexCreationException( string.Format( "Failed to initialize security descriptor. Win32 error num: '{0}'", lastError ) );
                    }

                    worked = Native.SetSecurityDescriptorDacl(ref securityDesc, true, IntPtr.Zero, false);
                    if( ! worked )
                    {
                        lastError = Marshal.GetLastWin32Error();
                        throw new MutexCreationException( string.Format( "Failed to set security descriptor DACL. Win32 error num: '{0}'", lastError ) );
                    }

                    Native.SECURITY_ATTRIBUTES secAttribs = new Native.SECURITY_ATTRIBUTES();
                    secAttribs.nLength = Marshal.SizeOf( secAttribs );
                    secAttribs.bInheritHandle = 1;

                    securityDescPtr = Marshal.AllocCoTaskMem( Marshal.SizeOf( securityDesc ) );
                    Marshal.StructureToPtr( securityDesc, securityDescPtr, false );
                    secAttribs.lpSecurityDescriptor = securityDescPtr;

                    mutexAttributesPtr = Marshal.AllocCoTaskMem( Marshal.SizeOf( secAttribs ) );
                    Marshal.StructureToPtr( secAttribs, mutexAttributesPtr, false );

                    hMutex = Native.CreateMutex( mutexAttributesPtr, initiallyOwned ? true : false, name );
                    lastError = Marshal.GetLastWin32Error();
                    createdNew = ( lastError != Native.ERROR_ALREADY_EXISTS );

                    if( hMutex == IntPtr.Zero )
                    {
                        // If we get here, some sort of unrecoverable error has presumably occurred.
                        // However, we will try one last time, in case it was merely some sort of race condition.
                        // Note that I do not believe that there is any opening for a race condition in the above code.
                        // Nevertheless, we have nothing to lose by giving it one last try.
                        hMutex = Native.OpenMutex( ( uint ) ( Native.SyncObjectAccess.MUTEX_MODIFY_STATE ), false, name );
                        createdNew = false;
                        if( hMutex == IntPtr.Zero )
                        {
                            lastError = Marshal.GetLastWin32Error();
                            throw new MutexCreationException( string.Format( "Unable to create or open mutex. Win32 error num: '{0}'", lastError ) );
                        }
                    }
                }

                return hMutex;
            }
            finally
            {
                if( mutexAttributesPtr != IntPtr.Zero )
                {
                    Marshal.FreeCoTaskMem( mutexAttributesPtr );
                }

                if( securityDescPtr != IntPtr.Zero )
                {
                    Marshal.FreeCoTaskMem( securityDescPtr );
                }
            }
        }
    }
```
