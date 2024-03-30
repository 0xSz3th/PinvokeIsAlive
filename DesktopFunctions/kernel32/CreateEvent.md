
## VB.NET Signature:
```cs
<DllImport("kernel32.dll", _
     EntryPoint:="CreateEventA")> _
    Public Shared Function CreateEvent( _
    ByVal lpEventAttributes As IntPtr, _
    ByVal bManualReset As Boolean, _
    ByVal bInitialState As Boolean, _
    ByVal lpName As String) As IntPtr
    End Function
```

## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern IntPtr CreateEvent(IntPtr lpEventAttributes, bool bManualReset, bool bInitialState, string lpName);
```

## Tips & Tricks:
```cs
AutoResetEvent are= new AutoResetEvent(false);
  are.Close();
  GC.ReRegisterForFinalize(are); 
  are.Handle= handle; // handle from CreateEvent
```

## Sample Code:
```cs
// Create an manual-reset event, which is initially set.
IntPtr myEventHandle = CreateEvent(IntPtr.Zero, false, true, "MyEvent");
if (myEventHandle == IntPtr.Zero)
{
   // An error occurred creating the handle... 
}
...
...
CloseHandle(myEventHandle);
```

## NOTE: This class needs some changes.  The CloseHandle call will destroy the event when the last handle is closed.  This makes it hard for one application to "lock" the event while making another wait on it since this class is always closing the handle.  An alternative that I found to work is to have the CreateEvent call in the constructor and implement IDisposable by moving the CloseHandle call to the Dispose method.
```cs
using System;
using System.Runtime.InteropServices;

namespace Utilities
{
    /// <summary>
    /// The NamedEvent class is to suppliment .NET's event classes with the ability to span
    /// processes in both .NET and Win32 with the same event signaling capability.
    /// 
    /// The NamedEvent class object provides the ability to wait on, pulse, set, and
    /// reset a named event. The event can be created with manual or automatic reset,
    /// and is always created with an initial state of reset(false).
    /// 
    /// The NamedEvent class will not leave a handle open past any method
    /// call, so garbage collection is irrelevant.
    /// 
    /// The NamedEvent class defines both instance methods and static methods.
    /// The static methods require a name, where as the instance methods contain the
    /// name in the object instance already. The static methods are also limited to
    /// the configuration of auto reset and initially not signaled.
    /// 
    /// The wait methods will wait on a single object, the named event, only. There
    /// is no multiple event support.
    ///
    /// Win32 security is a critical issue. This class does not support specifically
    /// identifying any security, other than the default process security context.
    /// This class is best suitable for processes run in the same security context,
    /// such as the desktop's interactive user account.
    /// </summary>

    public class NamedEvent
    {
    private string _EventName;
    private IntPtr _Handle;
    private IntPtr _Attributes = IntPtr.Zero;
    private bool _ManualReset;
    private bool _InitialState;
```

## NOTE: This class needs some changes.  The CloseHandle call will destroy the event when the last handle is closed.  This makes it hard for one application to "lock" the event while making another wait on it since this class is always closing the handle.  An alternative that I found to work is to have the CreateEvent call in the constructor and implement IDisposable by moving the CloseHandle call to the Dispose method.
```cs
public static uint INFINITE = 0xFFFFFFFF;
```

## NOTE: This class needs some changes.  The CloseHandle call will destroy the event when the last handle is closed.  This makes it hard for one application to "lock" the event while making another wait on it since this class is always closing the handle.  An alternative that I found to work is to have the CreateEvent call in the constructor and implement IDisposable by moving the CloseHandle call to the Dispose method.
```cs
////////// Interop information for managing a Win32 event ////////////

    [DllImport("kernel32.dll")]
    static extern IntPtr CreateEvent(IntPtr lpEventAttributes, bool bManualReset, bool bInitialState, string lpName);

    [DllImport("kernel32.dll", SetLastError=true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    static extern bool CloseHandle(IntPtr hObject);

    [DllImport("kernel32.dll")]
    static extern bool SetEvent(IntPtr hEvent);


    [DllImport("kernel32.dll")]
    static extern bool ResetEvent(IntPtr hEvent);

    [DllImport("kernel32.dll")]
    static extern bool PulseEvent(IntPtr hEvent);

    [DllImport("kernel32", SetLastError=true, ExactSpelling=true)]
    internal static extern Int32 WaitForSingleObject(IntPtr handle, Int32 milliseconds);
```

## NOTE: This class needs some changes.  The CloseHandle call will destroy the event when the last handle is closed.  This makes it hard for one application to "lock" the event while making another wait on it since this class is always closing the handle.  An alternative that I found to work is to have the CreateEvent call in the constructor and implement IDisposable by moving the CloseHandle call to the Dispose method.
```cs
/// <summary>
    /// Create a NamedEvent object with the name of the event, and assume auto reset with
    /// an initial state of reset.
    /// </summary>
    public NamedEvent(string EventName ) : this( EventName, false ) {}

    /// <summary>
    /// Create a NamedEvent object with the name of the event and the auto reset property,
    /// assuming an initial state of reset.
    /// </summary>
    public NamedEvent(string EventName, bool ManualReset )
    {
        _EventName = EventName;
        _ManualReset = ManualReset;
        _InitialState = false;
    }

    /// <summary>
    /// Wait for the event to signal to a maximum period of TimeoutInSecs total seconds.
    /// Returns true if the event signaled, false if timeout occurred.
    /// </summary>
    public bool Wait( int TimeoutInSecs )
    {
        _Handle = CreateEvent( _Attributes, _ManualReset, _InitialState, _EventName );
        int rc = WaitForSingleObject( _Handle, TimeoutInSecs * 1000 );
        CloseHandle( _Handle );
        return rc == 0;
    }

    /// <summary>
    /// Pulse the named event, which results in a single waiting thread to exit the Wait method.
    /// </summary>
    public bool Pulse()
    {
        _Handle = CreateEvent( _Attributes, _ManualReset, _InitialState, _EventName );
        PulseEvent( _Handle );
        CloseHandle( _Handle );
        return _Handle != IntPtr.Zero;
    }

    /// <summary>
    /// Set the named event to a signaled state. The Wait() method will not block any
    /// thread as long as the event is in a signaled state.
    /// </summary>
    public void Set()
    {
        _Handle = CreateEvent( _Attributes, _ManualReset, _InitialState, _EventName );
        SetEvent( _Handle );
        CloseHandle( _Handle );
    }

    /// <summary>
    /// Reset the named event to a non signaled state. The Wait() method will block
    /// any thread that enters it as long as the event is in a non signaled state.
    /// </summary>
    public void Reset()
    {
        _Handle = CreateEvent( _Attributes, _ManualReset, _InitialState, _EventName );
        ResetEvent( _Handle );
        CloseHandle( _Handle );
    }
```

## NOTE: This class needs some changes.  The CloseHandle call will destroy the event when the last handle is closed.  This makes it hard for one application to "lock" the event while making another wait on it since this class is always closing the handle.  An alternative that I found to work is to have the CreateEvent call in the constructor and implement IDisposable by moving the CloseHandle call to the Dispose method.
```cs
/// <summary>
    /// Wait for the event with the given name to signal to a maximum period of TimeoutInSecs total seconds.
    /// Returns true if the event signaled, false if timeout occurred.
    /// </summary>
    static public bool Wait( int TimeoutInSecs, string Name )
    {
        return (new NamedEvent(Name)).Wait( TimeoutInSecs );
    }

    /// <summary>
    /// Pulse the event with the given name, which results in a single waiting thread to exit the Wait method.
    /// </summary>
    static public bool Pulse(string Name) { return (new NamedEvent(Name)).Pulse(); }

    /// <summary>
    /// Set the event with the given name to a signaled state. The Wait() method will not block
    /// any threads as long as the event is in a signaled state.
    /// </summary>
    static public void Set(string Name) { (new NamedEvent(Name)).Set(); }

    /// <summary>
    /// Reset the event with the given name to a non signaled state. The Wait() method will block
    /// any thread that enters it as long as the event is in a non signaled state.
    /// </summary>
    static public void Reset( string Name) { (new NamedEvent(Name)).Reset(); }
    }
}
```
