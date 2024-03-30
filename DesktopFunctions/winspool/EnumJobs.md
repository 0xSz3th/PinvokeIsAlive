
## C# Signature:
```cs
[DllImport("Winspool.drv", SetLastError=true, EntryPoint="EnumJobsA")]
public static extern bool EnumJobs(
   IntPtr hPrinter,                    // handle to printer object
   UInt32 FirstJob,                // index of first job
   UInt32 NoJobs,                // number of jobs to enumerate
   UInt32 Level,                    // information level
   IntPtr pJob,                        // job information buffer
   UInt32 cbBuf,                    // size of job information buffer
   out UInt32 pcbNeeded,    // bytes received or required
   out UInt32 pcReturned    // number of jobs received
);
```

## VB Signature:
```cs
Public Declare Function EnumJobs Lib "winspool.drv" Alias "EnumJobsA" _
    (ByVal hPrinter As IntPtr, _
    ByVal FirstJob As UInt32, _
    ByVal NoJobs As UInt32, _
    ByVal Level As UInt32, _
    ByVal pJob As IntPtr, _
    ByVal cdBuf As UInt32, _
    ByRef pcbNeeded As UInt32, _
    ByRef pcReturned As UInt32) _
    As Long
```

## User-Defined Types:
```cs
<StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> Structure JOB_INFO_1
    Public JobId As Integer
    Public pPrinterName As IntPtr
    Public pMachineName As IntPtr
    Public pUserName As IntPtr
    Public pDocument As IntPtr
    Public pDataType As IntPtr
    Public pStatus As IntPtr
    Public Status As Integer
    Public Priority As Integer
    Public Position As Integer
    Public TotalPages As Integer
    Public PagesPrinter As Integer
    Public Submitted As SYSTEMTIME
    End Structure

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Auto)> Structure SYSTEMTIME
    Public wYear As Short
    Public wMonth As Short
    Public wDayOfWeek As Short
    Public wDay As Short
    Public wHour As Short
    Public wMinute As Short
    Public wSecond As Short
    Public wMilliseconds As Short
    End Structure
```

## Sample Code:
```cs
Imports System.Runtime.InteropServices

    Public Class WINAPI

    Public Function DatatoDeserial(ByVal datas() As Byte, ByVal type_to_change As Type, _
    ByVal NumJub As Long) As Object
    'Returns the size of the JOB_INFO_1 structure
    Dim Data_to_Size As Long = Marshal.SizeOf(type_to_change)
    If Data_to_Size > datas.Length Then
        Return Nothing
    End If

    Dim buffer As IntPtr = Marshal.AllocHGlobal(CInt(Data_to_Size))
    Dim startindex As Long
    Dim i As Integer
    For i = 0 To NumJub - 1
        If i = 0 Then
        startindex = 0
        Else
        startindex = startindex + Data_to_Size
        End If
    Next
    'Copy data from the datas array to the unmanaged memory pointer.
    Marshal.Copy(datas, startindex, buffer, Data_to_Size)

    'Marshal data from the buffer pointer to a managed object.
    Dim result_obj As Object = Marshal.PtrToStructure(buffer, type_to_change)
    'Free the memory that is allocated from the unmanaged memory.
    Marshal.FreeHGlobal(buffer)
    Return result_obj
    End Function

    'Include Structures Here

    End Class

    Sub RetrieveJobs()

    Dim API As New WINAPI
    Dim JI1 As New WINAPI.JOB_INFO_1
    Dim JI1Size As Integer = Marshal.SizeOf(JI1)
    Dim lNeeded As UInt32
    Dim lReturned As UInt32
    Dim lRetrieve As UInt32
    Dim buffer As IntPtr
    Dim btbuffer As Byte()
    Dim rt As Integer
    'this call retrieves no data, but does retrieve the about of buffer needed
    'this call will always fail (return non-0)
    WINAPI.EnumJobs(hPQH, 0, 99, 1, Nothing, 0, lNeeded, lReturned)
    'if there is data...
    If lNeeded > 0 Then
        'keep size of buffer in new var
        lRetrieve = lNeeded
        'allocate buffer size
        buffer = Marshal.AllocHGlobal(CInt(lNeeded))
        'actually retrieve the buffer
        rt = WINAPI.EnumJobs(hPQH, 0, 99, 1, buffer, lRetrieve, lNeeded, lReturned)
        If rt <> 0 Then 'if call succeeds you have a valid job array in buffer
        'capture buffer into a byte array
        ReDim btbuffer(lRetrieve)
        Marshal.Copy(buffer, btbuffer, 0, lRetrieve)
        'deserialize data one job at a time
        For I As Integer = 1 To lReturned
            JI1 = API.DatatoDeserial(btbuffer, JI1.GetType, I)
            MsgBox(Marshal.PtrToStringAnsi(JI1.pDocument))
        Next
        End If
        'FreeFile up the original buffer
        Marshal.FreeHGlobal(buffer)
    Else
        MsgBox("No Jobs Enumerated")

    End If

    End Sub
```
