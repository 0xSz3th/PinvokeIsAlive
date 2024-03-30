
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
public static extern IntPtr FindWindowEx(IntPtr parentHandle, IntPtr hWndChildAfter, string className,  string windowTitle);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Private Shared Function FindWindowEx(ByVal parentHandle As IntPtr, _
                      ByVal childAfter As IntPtr, _
                      ByVal lclassName As String, _
                      ByVal windowTitle As String) As IntPtr
End Function
```

## Sample Code:
```cs
/// <summary>
/// Gets the handle to the horizontal scroll bar.
/// </summary>
/// <param name="parentControl">The parent window of the scrollbar.</param>
/// <returns>Handle to the scrollbar window.</returns>
private IntPtr GetHandleToHorizontalScrollBar(Control parent)
{
    // Locals
    IntPtr childHandle;
    string appDomainHexedHash;

    // Get the hexadecimal value of AppDomain hash code.
    // This value is dynamically appended to the window class name of the child window
    // for .NET Windows Forms.  This name is viewable via the Spy++ tool.
    appDomainHexedHash = AppDomain.CurrentDomain.GetHashCode().ToString("x");

    // Find window handle
    childHandle = FindWindowEx(
        parent.Handle,    // Parent handle
        IntPtr.Zero,    // Child window after which to seek
        "WindowsForms10.SCROLLBAR.app.0." + appDomainHexedHash, // Class name to seek (viewable in the Spy++ tool)
        IntPtr.Zero);    // Window title to seek

    // Return handle
    return childHandle;
}

private string GetUrlFromIE()
{
    IntPtr windowHandle = GetForegroundWindow();
    IntPtr childHandle;
    String strUrlToReturn = "";

    //try to get a handle to IE's toolbar container
    childHandle = FindWindowEx(windowHandle,IntPtr.Zero,"WorkerW",IntPtr.Zero);
    if(childHandle != IntPtr.Zero)
    {
        //get a handle to address bar
        childHandle = FindWindowEx(childHandle,IntPtr.Zero,"ReBarWindow32",IntPtr.Zero);
        if(childHandle != IntPtr.Zero)
        {
            // get a handle to combo boxex
            childHandle = FindWindowEx(childHandle, IntPtr.Zero, "ComboBoxEx32", IntPtr.Zero);
            if(childHandle != IntPtr.Zero)
            {
                // get a handle to combo box
                childHandle = FindWindowEx(childHandle, IntPtr.Zero, "ComboBox", IntPtr.Zero);
                if(childHandle != IntPtr.Zero)
                {
                    //get handle to edit
                    childHandle = FindWindowEx(childHandle, IntPtr.Zero, "Edit", IntPtr.Zero);
                    if (childHandle != IntPtr.Zero)
                    {
                        strUrlToReturn = GetText(childHandle);
                    }
                }
            }
        }
    }
    return strUrlToReturn;
}
```
