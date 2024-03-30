
## C# Signature:
```cs
[DllImport("iphlpapi.dll", SetLastError=true)]
static extern int EnableRouter(IntPtr pHandle, ref System.Threading.NativeOverlapped pOverlapped);
```

## VB.NET Signature:
```cs
<DllImport("iphlpapi.dll", CharSet:=CharSet.Ansi)>
    Public Shared Function EnableRouter(pHandle As IntPtr, ByRef pOverlapped As OVERLAPPED) As Integer
    End Function
```

## Sample Code:
```cs
Private Const ERROR_IO_PENDING As Integer = 997

    <StructLayout(LayoutKind.Explicit, Size:=20)>
    Public Structure OVERLAPPED
    <FieldOffset(0)>
    Public Internal As UInt32
    <FieldOffset(4)>
    Public InternalHigh As UInt32
    <FieldOffset(8)>
    Public Offset As UInt32
    <FieldOffset(12)>
    Public OffsetHigh As UInt32
    <FieldOffset(8)>
    Public Pointer As IntPtr
    <FieldOffset(16)>
    Public hEvent As IntPtr
    End Structure

    <DllImport("iphlpapi.dll", CharSet:=CharSet.Ansi)>
    Public Shared Function EnableRouter(pHandle As IntPtr, ByRef pOverlapped As OVERLAPPED) As Integer
    End Function

    <DllImport("kernel32.dll", EntryPoint:="CreateEventA", CharSet:=CharSet.Unicode)>
    Public Shared Function CreateEvent(lpEventAttributes As IntPtr, ByVal bManualReset As Boolean, ByVal bInitialState As Boolean, ByVal lpName As String) As IntPtr
    End Function

    Private pOverlapped As OVERLAPPED ' <- Important! This should also be used when calling UnenableRouter() API Function.

    Private Sub Button2_Click(sender As Object, e As EventArgs) Handles Button2.Click
    ' OVERLAPPED strucutre fields can be NULLED except hEvent field.
    pOverlapped.hEvent = CreateEvent(IntPtr.Zero, False, False, "enablerouter")
    Dim RetVal As Integer = EnableRouter(IntPtr.Zero, pOverlapped)

    If RetVal = ERROR_IO_PENDING Then
        Console.WriteLine("Success!")
    Else
        Dim errorMessage As String = New Win32Exception(RetVal).Message
        Console.WriteLine("Error {0}", errorMessage)
    End If
    End Sub
```
