
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true)]
static extern IntPtr SetWindowsHookEx(HookType hookType, HookProc lpfn, IntPtr hMod, uint dwThreadId);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function SetWindowsHookEx(ByVal hookType As HookType, ByVal lpfn As HookProc, ByVal hMod As IntPtr, ByVal dwThreadId As UInteger) As IntPtr
End Function
```

## Notes:
```cs
IntPtr hHook;

using (Process process = Process.GetCurrentProcess())
using (ProcessModule module = process.MainModule)
{
    IntPtr hModule = GetModuleHandle(module.ModuleName);

    hHook = SetWindowsHookEx(HookType.WH_KEYBOARD_LL, hook, hModule, 0);
}
```

## Sample Code:
```cs
// this sample installs a keyboard hook

using System.Windows.Forms;
public class MyClass
{
     private HookProc myCallbackDelegate = null;

     public MyClass()
     {
     // initialize our delegate
     this.myCallbackDelegate = new HookProc(this.MyCallbackFunction);

     // setup a keyboard hook
     SetWindowsHookEx(HookType.WH_KEYBOARD, this.myCallbackDelegate, IntPtr.Zero, AppDomain.GetCurrentThreadId());
     }

     [DllImport("user32.dll")]
     protected static extern IntPtr SetWindowsHookEx(HookType code, HookProc func, IntPtr hInstance, int threadID);

     [DllImport("user32.dll")]
     static extern int CallNextHookEx(IntPtr hhk, int nCode, IntPtr wParam, IntPtr lParam);

     private int MyCallbackFunction(int code, IntPtr wParam, IntPtr lParam)
     {
    if (code < 0) {
        //you need to call CallNextHookEx without further processing
        //and return the value returned by CallNextHookEx
        return CallNextHookEx(IntPtr.Zero, code, wParam, lParam);
    }
     // we can convert the 2nd parameter (the key code) to a System.Windows.Forms.Keys enum constant
     Keys keyPressed = (Keys)wParam.ToInt32();
     Console.WriteLine(keyPressed);
    //return the value returned by CallNextHookEx
    return CallNextHookEx(IntPtr.Zero, code, wParam, lParam);
     }
}
```

## VB.NET:
```cs
' My sample installs a keyboard hook
Imports System.Windows.Forms
Imports System.Runtime.InteropServices

Public Class MyClass1
    Delegate Function HookProc(ByVal code As Integer, ByVal wParam As IntPtr, ByVal lParam As IntPtr) As Integer

    Private myCallbackDelegate As HookProc = Nothing

    Public Sub New()
    ' initialize our delegate
    Me.myCallbackDelegate = New HookProc(AddressOf Me.MyCallbackFunction)

    ' setup a keyboard hook
    SetWindowsHookEx(HookType.WH_KEYBOARD, Me.myCallbackDelegate, IntPtr.Zero, AppDomain.GetCurrentThreadId())
    End Sub

    <DllImport("user32.dll")> _
    Friend Shared Function SetWindowsHookEx(ByVal idHook As Integer, ByVal lpfn As HookProc, ByVal hInstance As IntPtr, ByVal threadId As Integer) As Integer
    End Function

    <DllImport("user32.dll")> _
    Friend Shared Function CallNextHookEx(ByVal hhk As intptr, ByVal nCode As Integer, ByVal wParam As intptr, ByVal lParam As intptr) As Integer
    End Function

    Private Function MyCallbackFunction(ByVal code As Integer, ByVal wParam As intptr, ByVal lParam As intptr) As Integer
    If (code < 0) Then
        'you need to call CallNextHookEx without further processing
        'and return the value returned by CallNextHookEx
        Return CallNextHookEx(IntPtr.Zero, code, wParam, lParam)    'unt
    End If
    ' we can convert the 2nd parameter (the key code) to a System.Windows.Forms.Keys enum constant
    Dim keyPressed As Keys = CType(wParam.ToInt32, Keys)
    Console.WriteLine(keyPressed)
    'return the value returned by CallNextHookEx
    Return CallNextHookEx(IntPtr.Zero, code, wParam, lParam)
    End Function
End Class
```
