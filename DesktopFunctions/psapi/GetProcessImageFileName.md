
## C# Signature:
```cs
[DllImport("psapi.dll")]
static extern uint GetProcessImageFileName(
    IntPtr hProcess, 
    [Out] StringBuilder lpImageFileName, 
    [In] [MarshalAs(UnmanagedType.U4)] int nSize
);
```

## VB Signature:
```cs
Declare Function GetProcessImageFileName Lib "psapi.dll" 
<DllImport("psapi.dll")> _
Public Shared Function GetProcessImageFileName(
    ByVal hProcess As IntPtr,
    <Out> lpImageFileName As StringBuilder,
    <[In]> <MarshalAs(UnmanagedType.U4)> uSize As Integer
) As UInteger
End Function
```

## Sample Code:
```cs
uint pid = 0;
StringBuilder fileName = new StringBuilder(2000);

/** get the handle for point under cursor **/
IntPtr hWnd = WindowFromPoint(pt);

/** Need to get the process ID from handle under cursor **/
GetWindowThreadProcessId(hWnd, out pid);

/** Hook into process **/
IntPtr pic = OpenProcess(NativeMethods.ProcessAccessFlags.All, true, (int)pid);

/** This gets the filename of the process image. Path is in device format **/
GetProcessImageFileName(pic, fileName, 2000);

MessageBox.Show(fileName.ToString());
```
