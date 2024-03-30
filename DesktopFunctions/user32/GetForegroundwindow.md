
## C# Signature:
```cs
/// <summary>
    ///     Retrieves a handle to the foreground window (the window with which the user is currently working). The system
    ///     assigns a slightly higher priority to the thread that creates the foreground window than it does to other threads.
    ///     <para>See https://msdn.microsoft.com/en-us/library/windows/desktop/ms633505%28v=vs.85%29.aspx for more information.</para>
    /// </summary>
    /// <returns>
    ///     C++ ( Type: Type: HWND )<br /> The return value is a handle to the foreground window. The foreground window
    ///     can be NULL in certain circumstances, such as when a window is losing activation.
    /// </returns>
[DllImport("user32.dll")]
private static extern IntPtr GetForegroundWindow();
```

## VB.NET Signature:
```cs
''' <summary>The GetForegroundWindow function returns a handle to the foreground window.</summary>
''' <returns>The return value is a handle to the foreground window. The foreground window can be NULL in certain circumstances, such as when a window is losing activation. </returns>
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function GetForegroundWindow() As IntPtr
End Function
```

## VB.NET Signature Alternative
```cs
''' <summary>
''' Retrieves a handle to the foreground window (the window with which the user is currently working). The system assigns a slightly higher priority to the thread that creates the foreground window than it does to other threads. 
''' </summary>
''' <returns>The return value is a handle to the foreground window. The foreground window can be NULL in certain circumstances, such as when a window is losing activation. </returns>
''' <remarks>http://msdn.microsoft.com/en-us/library/ms633505%28v=vs.85%29.aspx</remarks>
Private Declare Function GetForegroundWindow Lib "user32.dll" () As IntPtr
```

## VB Signature:
```cs
Public Declare Function GetForegroundWindow Lib "user32" () As Long
```

## F# Signature
```cs
[<DllImport("user32")>]
extern IntPtr GetForegroundWindow()
```

## Sample Code:
```cs
public ApplicationState AppState
{
    get
    {
        Process[] processCollection = Process.GetProcessesByName(ProcessName);
        if(processCollection != null && processCollection.Length  >= 1 && 
            processCollection[0] != null)
        {
            IntPtr activeWindowHandle = Win32.GetForegroundWindow();
            //Optional int ProcessID;
            //Optional Win32.GetWindowThreadProcessId(GetForegroundWindow(),out ProcessID)
            foreach(Process wordProcess in processCollection)
            {
                //Optional if( ProcessID == wordProcess.Id ) return ApplicationState.Focused;
                if(wordProcess.MainWindowHandle == activeWindowHandle)
                {
                    return ApplicationState.Focused;
                }
            }
            return ApplicationState.Running;
        }
        return ApplicationState.NotRunning;
    }
}
```
