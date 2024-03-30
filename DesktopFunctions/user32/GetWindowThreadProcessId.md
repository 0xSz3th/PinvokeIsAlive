
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern uint GetWindowThreadProcessId(IntPtr hWnd, out uint lpdwProcessId);

// When you don't want the ProcessId, use this overload and pass IntPtr.Zero for the second parameter
[DllImport("user32.dll")]
static extern uint GetWindowThreadProcessId(IntPtr hWnd, IntPtr ProcessId);
```

## VB.Net Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function GetWindowThreadProcessId(ByVal hwnd As IntPtr, _
                          ByRef lpdwProcessId As Integer) As Integer
End Function
```

## VB.Net Signature:
```cs
''' <summary>
    ''' Retrieves the identifier of the thread that created the specified window and, optionally, the identifier of the process that created the window. 
    ''' </summary>
    ''' <param name="hwnd">A handle to the window. </param>
    ''' <param name="lpdwProcessId">A pointer to a variable that receives the process identifier. If this parameter is not NULL, GetWindowThreadProcessId copies the identifier of the process to the variable; otherwise, it does not. </param>
    ''' <returns>The return value is the identifier of the thread that created the window. </returns>
    ''' <remarks>http://msdn.microsoft.com/en-us/library/ms633522%28v=vs.85%29.aspx</remarks>
    Private Declare Auto Function GetWindowThreadProcessId Lib "user32.dll" (ByVal hwnd As IntPtr, _
                  ByRef lpdwProcessId As Integer) As Integer
```

## Sample Code (VB):
```cs
If objAcc Is Nothing Then
  objAcc = New Application
  Dim lngPid As Integer
  Dim lngAccessHwnd As IntPtr = New IntPtr(objAcc.hWndAccessApp)
  GetWindowThreadProcessId(lngAccessHwnd, lngPid)
End If
```

## Sample Code (VB):
```cs
Public Module MainModule

    Public Sub Main()

        Dim oProcess As Process = GetClipboardProcess()

        Debug.WriteLine(oProcess.ProcessName)
        Debug.WriteLine(oProcess.MainModule.FileName)

    End Sub

    Public Declare Unicode Function GetClipboardOwner Lib "user32" () As IntPtr
    Public Declare Auto Function GetWindowThreadProcessId Lib "user32" (ByVal hwnd As IntPtr, ByRef lpdwProcessId As IntPtr) As IntPtr

    Public Function GetClipboardProcess() As Process
        Dim oResult As Process = Nothing

        Dim hOwner As IntPtr = GetClipboardOwner()

        If hOwner <> IntPtr.Zero Then

        Dim iProcessID As IntPtr

        GetWindowThreadProcessId(hOwner, iProcessID)

        oResult = Process.GetProcessById(iProcessID.ToInt32)

        End If

        Return oResult
    End Function

    End Module
```

## Sample Code (C#):
```cs
IntPtr pID = GetWindowThreadProcessId(GetForegroundWindow(), IntPtr.Zero);
```

## Sample Code (C#):
```cs
int processID = 0;
int threadID = GetWindowThreadProcessId(hWnd, out processID);
```
