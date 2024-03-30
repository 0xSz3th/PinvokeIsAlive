
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern uint QueryDosDevice(string lpDeviceName, IntPtr lpTargetPath, uint ucchMax);
```

## Alternate C# signature:
```cs
[DllImport("kernel32.dll", SetLastError = true)]
static extern uint QueryDosDevice(string lpDeviceName, StringBuilder lpTargetPath, int ucchMax);
```

## Alternate C# signature useful for retrieving list of devices
```cs
[DllImport("Kernel32.dll")]
static extern uint QueryDosDevice([In, Optional] string lpDeviceName, [Out]byte[] rv, uint ucchMax);
```

## VB.NET Signature:
```cs
<DllImport("Kernel32.dll", EntryPoint:="QueryDosDevice")>
Public Shared Function QueryDosDevice(lpDeviceName As String, lpTargetPath As System.Text.StringBuilder, ucchMax As Integer) As Integer
End Function
```

## VB.NET Sample Code:
```cs
' Use the VB.NET signature above with this code. Converting the C#
' signatures will not work.
Private Function QueryDosDevice(ByVal device As String) As List(Of String)

    Dim returnSize As Integer = 0
    Dim maxSize As UInteger = 65536
    Dim allDevices As String = Nothing
    Dim mem As IntPtr
    Dim retval() As String = Nothing
    Dim results As New List(Of String)

    ' Convert an empty string into Nothing, so 
    ' QueryDosDevice will return everything available.
    If device.Trim = "" Then device = Nothing

    While returnSize = 0
        mem = Marshal.AllocHGlobal(CInt(maxSize))
        If mem <> IntPtr.Zero Then
        Try
            returnSize = CInt(QueryDosDevice(device, mem, maxSize))
            If returnSize <> 0 Then
            allDevices = Marshal.PtrToStringAuto(mem, returnSize)
            retval = allDevices.Split(ControlChars.NullChar)
            Exit Try
            Else
            ' This query produced no results. Exit the loop.
            returnSize = -1
            End If
        Finally
            Marshal.FreeHGlobal(mem)
        End Try
        Else
        Throw New OutOfMemoryException()
        End If
    End While

    If retval IsNot Nothing Then
        For Each result As String In retval
        If result.Trim <> "" Then results.Add(result)
        Next
    End If

    Return results
End Function
```

## C# Sample Code:
```cs
private static string[] QueryDosDevice()
{
    // Allocate some memory to get a list of all system devices.
    // Start with a small size and dynamically give more space until we have enough room.
    int returnSize = 0;
    int maxSize = 100;
    string allDevices = null;
    IntPtr mem;
    string [] retval = null;

    while(returnSize == 0)
    {
        mem = Marshal.AllocHGlobal(maxSize);
        if(mem != IntPtr.Zero)
        {
            // mem points to memory that needs freeing
            try
            {
                returnSize = QueryDosDevice(null, mem, maxSize);
                if(returnSize != 0)
                {
                    allDevices = Marshal.PtrToStringAnsi(mem, returnSize);
                    retval = allDevices.Split('\0');
                    break;    // not really needed, but makes it more clear...
                }
                else if(GetLastError() == ERROR_INSUFFICIENT_BUFFER)
                //maybe better
                //else if( Marshal.GetLastWin32Error() == ERROR_INSUFFICIENT_BUFFER)
                //ERROR_INSUFFICIENT_BUFFER = 122;
                {
                    maxSize *= 10;
                }
                else
                {
                    Marshal.ThrowExceptionForHR(GetLastError());
                }
            }
            finally
            {
                Marshal.FreeHGlobal(mem);
            }
        }
        else
        {
            throw new OutOfMemoryException();
        }
    }
    return retval;
}
```

## Sample Code for alternate C# signature:
```cs
private static string GetRealPath(string path)
{
    string realPath;
    StringBuilder pathInformation = new StringBuilder(250);

    // Get the drive letter of the 
     string driveLetter = Path.GetPathRoot(path).Replace("\\", "");
     QueryDosDevice(driveLetter, pathInformation, 250);

    // If drive is substed, the result will be in the format of "\??\C:\RealPath\".
    if (pathInformation.ToString().Contains("\\??\\"))
    {
       // Strip the \??\ prefix.
       string realRoot = pathInformation.ToString().Remove(0, 4);

       //Combine the paths.
       realPath = Path.Combine(realRoot, path.Replace(Path.GetPathRoot(path), ""));
    }
    else
    {
       realPath = path;
    }
    return realPath;
}
```

## Sample C# code retrieving list of devices
```cs
public static string[] QueryDevice(string driveLetter=null)
{
    byte[] buffer = new byte[4096*32];
    uint len = QueryDosDevice(driveLetter, buffer, (uint)buffer.Length);
    if (len == 0)
    return null;
    string rv = ASCIIEncoding.ASCII.GetString(buffer, 0, (int)len-2); // two terminating nulls
    return rv.Split("\0".ToCharArray());
}
```
