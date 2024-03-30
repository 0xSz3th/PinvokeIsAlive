
## C# Signature:
```cs
[DllImport("iphlpapi.dll", SetLastError=true)]
static extern int UnenableRouter(ref System.Threading.NativeOverlapped pOverlapped, IntPtr lpdwEnableCount);
```

## VB.NET Signature:
```cs
<DllImport("iphlpapi.dll", CharSet:=CharSet.Ansi)>
    Public Shared Function UnenableRouter(pOverlapped As IntPtr, ByRef lpdwEnableCount As Long) As Integer
    End Function
```

## Sample Code:
```cs
Private Const NO_ERROR As Integer = 0
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
    Public Shared Function UnenableRouter(pOverlapped As IntPtr, ByRef lpdwEnableCount As Long) As Integer
    End Function

    <DllImport("kernel32.dll")>
    Public Shared Function CloseHandle(ByVal hwn As IntPtr) As Long
    End Function

    Private pOverlapped As OVERLAPPED <- Important! Created from EnableRouter() call.

    Private Sub Button3_Click(sender As Object, e As EventArgs) Handles Button3.Click
    Dim count As Long
    Dim pOverlappedPtr As IntPtr
    Dim RetVal As Integer
    Dim size As Integer
    Try
        size = Marshal.SizeOf(pOverlapped)
        If pOverlapped.hEvent = IntPtr.Zero Then Exit Sub ' We don't have the handle.
        pOverlappedPtr = Marshal.AllocHGlobal(size)
        Marshal.StructureToPtr(pOverlapped, pOverlappedPtr, True)

        RetVal = UnenableRouter(pOverlappedPtr, count)
        If RetVal = NO_ERROR Then
        Console.WriteLine("Success!")
        Else
        Dim errorMessage As String = New Win32Exception(RetVal).Message
        Console.WriteLine(errorMessage)
        End If
        If pOverlappedPtr <> IntPtr.Zero Then CloseHandle(pOverlapped.hEvent)
    Catch ex As Exception
        Console.WriteLine(ex.ToString)
    Finally
        Marshal.FreeHGlobal(pOverlappedPtr)
    End Try
        End Sub
```
