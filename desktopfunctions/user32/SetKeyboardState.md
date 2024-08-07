
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool SetKeyboardState(byte [] lpKeyState);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)>
    Private Shared Function SetKeyboardState(ByVal lpKeyState() As Byte) As Boolean
    End Function
```

## Sample Code:
```cs
' struct to call API
    Private Structure OSVERSIONINFO

    Dim dwOSVersionInfoSize As Integer
    Dim dwMajorVersion As Integer
    Dim dwMinorVersion As Integer
    Dim dwBuildNumber As Integer
    Dim dwPlatformId As Integer

    <VBFixedString(128), System.Runtime.InteropServices.MarshalAs(System.Runtime.InteropServices.UnmanagedType.ByValTStr, SizeConst:=128)> Public szCSDVersion As String '  Maintenance string for PSS usage

    End Structure

    Private Declare Function GetVersionEx Lib "kernel32" Alias "GetVersionExA" (ByRef lpVersionInformation As OSVERSIONINFO) As Integer
    Private Declare Sub keybd_event Lib "user32" (ByVal bVk As Byte, ByVal bScan As Byte, ByVal dwFlags As Integer, ByVal dwExtraInfo As Integer)
    Private Declare Function GetKeyboardState Lib "user32" (ByRef pbKeyState As Byte) As Integer
    Private Declare Function SetKeyboardState Lib "user32" (ByRef lppbKeyState As Byte) As Integer

    'const
    Const VK_NUMLOCK As Short = &H90S
    Const VK_SCROLL As Short = &H91S
    Const VK_CAPITAL As Short = &H14S
    Const KEYEVENTF_EXTENDEDKEY As Short = &H1S
    Const KEYEVENTF_KEYUP As Short = &H2S
    Const VER_PLATFORM_WIN32_NT As Short = 2
    Const VER_PLATFORM_WIN32_WINDOWS As Short = 1

    Private Sub cmdNumLock_Click(ByVal eventSender As System.Object, ByVal eventArgs As System.EventArgs) Handles cmdNumLock.Click

    Dim o As OSVERSIONINFO
    Dim NumLockState As Boolean

    o.dwOSVersionInfoSize = Len(o)

    GetVersionEx(o)
    Dim keys(255) As Byte

    GetKeyboardState(keys(0))

    'NUMLOCK
    NumLockState = keys(VK_NUMLOCK)

    'check NUMLOCK state
    If NumLockState <> True Then 'if disabled then enable it
        If o.dwPlatformId = VER_PLATFORM_WIN32_WINDOWS Then '=== Win95/98
        keys(VK_NUMLOCK) = 1
        SetKeyboardState(keys(0))
        ElseIf o.dwPlatformId = VER_PLATFORM_WIN32_NT Then  '=== WinNT
        'Key Press
        keybd_event(VK_NUMLOCK, &H45S, KEYEVENTF_EXTENDEDKEY Or 0, 0)
        'Key Release
        keybd_event(VK_NUMLOCK, &H45S, KEYEVENTF_EXTENDEDKEY Or KEYEVENTF_KEYUP, 0)
        End If
    Else 'se estiver ativado -> if enabled then disable it
        If o.dwPlatformId = VER_PLATFORM_WIN32_WINDOWS Then '=== Win95/98
        keys(VK_NUMLOCK) = 0
        SetKeyboardState(keys(0))
        ElseIf o.dwPlatformId = VER_PLATFORM_WIN32_NT Then  '=== WinNT
        'Key Press
        keybd_event(VK_NUMLOCK, &H45S, KEYEVENTF_EXTENDEDKEY Or 0, 0)
        'Key Release
        keybd_event(VK_NUMLOCK, &H45S, KEYEVENTF_EXTENDEDKEY Or KEYEVENTF_KEYUP, 0)
        End If
    End If

    End Sub
```

## Sample Code:
```cs
Private Sub cmdCapsLock_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles cmdCapsLock.Click

    Dim o As OSVERSIONINFO
    Dim CapsLockState As Boolean

    o.dwOSVersionInfoSize = Len(o)

    GetVersionEx(o)
    Dim keys(255) As Byte

    GetKeyboardState(keys(0))

    'CAPSLOCK
    CapsLockState = keys(VK_CAPITAL)

    'check CAPSLOCK state
    If CapsLockState <> True Then 'if disabled then enable it
        If o.dwPlatformId = VER_PLATFORM_WIN32_WINDOWS Then '=== Win95/98
        keys(VK_CAPITAL) = 1
        SetKeyboardState(keys(0))
        ElseIf o.dwPlatformId = VER_PLATFORM_WIN32_NT Then  '=== WinNT
        'Key Press
        keybd_event(VK_CAPITAL, &H45S, KEYEVENTF_EXTENDEDKEY Or 0, 0)
        'Key Release
        keybd_event(VK_CAPITAL, &H45S, KEYEVENTF_EXTENDEDKEY Or KEYEVENTF_KEYUP, 0)
        End If
    Else 'se estiver ativado -> if enabled then disable it
        If o.dwPlatformId = VER_PLATFORM_WIN32_WINDOWS Then '=== Win95/98
        keys(VK_CAPITAL) = 0
        SetKeyboardState(keys(0))
        ElseIf o.dwPlatformId = VER_PLATFORM_WIN32_NT Then  '=== WinNT
        'Key Press
        keybd_event(VK_CAPITAL, &H45S, KEYEVENTF_EXTENDEDKEY Or 0, 0)
        'Key Release
        keybd_event(VK_CAPITAL, &H45S, KEYEVENTF_EXTENDEDKEY Or KEYEVENTF_KEYUP, 0)
        End If
    End If

    End Sub
```
