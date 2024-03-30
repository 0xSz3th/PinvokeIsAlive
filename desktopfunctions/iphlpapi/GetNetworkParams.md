
## C# Signature:
```cs
[DllImport("iphlpapi.dll", CharSet=CharSet.Ansi)]
public static extern int GetNetworkParams(IntPtr pFixedInfo, ref UInt32 pBufOutLen);
```

## VB.NET Signature:
```cs
<DllImport("iphlpapi.dll", CharSet:=CharSet.Ansi)>
    Public Shared Function GetNetworkParams(pFixedInfo As IntPtr, ByRef pBufOutLen As Integer) As Integer
    End Function
```

## Sample Code:
```cs
infoPtr = Marshal.AllocHGlobal(Convert.ToInt32(infoLen));
    ret = GetNetworkParams(infoPtr, ref infoLen);

    if (ret == ERROR_BUFFER_OVERFLOW)
    {
        //try again w/ bigger buffer:
        Marshal.FreeHGlobal(infoPtr);
        continue;
    }

    if (ret == ERROR_SUCCESS)
        break;

    throw new ApplicationException("An error occurred while fetching adapter information.", new Win32Exception(Convert.ToInt32(ret)));
```

## Sample Code:
```cs
Private Const ERROR_SUCCESS As Long = 0
    Private Const ERROR_BUFFER_OVERFLOW As Integer = 111

    Private Const MAX_HOSTNAME_LEN As Integer = 128
    Private Const MAX_SCOPE_ID_LEN As Integer = 256
    Private Const MAX_DOMAIN_NAME_LEN As Integer = 128

    <StructLayout(LayoutKind.Sequential, CharSet:=CharSet.Ansi)>
    Private Structure FIXED_INFO
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_HOSTNAME_LEN + 4)>
    Public HostName As String
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_DOMAIN_NAME_LEN + 4)>
    Public DomainName As String
    Public CurrentDnsServer As IntPtr
    Public DnsServerList As IP_ADDR_STRING
    Public NodeType As UInteger
    <MarshalAs(UnmanagedType.ByValTStr, SizeConst:=MAX_SCOPE_ID_LEN + 4)>
    Public ScopeId As String
    Public EnableRouting As Boolean
    Public EnableProxy As Boolean
    Public EnableDns As Boolean
    End Structure

    <DllImport("iphlpapi.dll", CharSet:=CharSet.Ansi)>
    Private Shared Function GetNetworkParams(pFixedInfo As IntPtr, ByRef pBufOutLen As Integer) As Integer
    End Function

    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
    Dim infoPtr As IntPtr = IntPtr.Zero
    Dim infoLen As Integer
    '      Dim bufOF As Boolean = True
    Dim ret As Integer

    Try
        '       Do While bufOF
        ret = GetNetworkParams(infoPtr, infoLen)
        If ret = ERROR_BUFFER_OVERFLOW Then
        infoPtr = Marshal.AllocHGlobal(infoLen)
        ret = GetNetworkParams(infoPtr, infoLen)
        End If
```

## Sample Code:
```cs
If ret = ERROR_BUFFER_OVERFLOW Then
        ElseIf ret = ERROR_SUCCESS Then
        Dim info As FIXED_INFO = Marshal.PtrToStructure(infoPtr, GetType(FIXED_INFO))
        ' We can now access the FIXED_INFO fields here.
        Console.WriteLine("Enable Routing: {0}", info.EnableRouting) ' CBool(info.EnableRouting))
        Else
        Dim errorMessage As String = New Win32Exception(ret).Message
            Console.WriteLine("Error {0}", errorMessage)
        End If
        '   Loop

    Catch ex As Exception
        Console.WriteLine(ex.ToString)
    Finally
        'Try again w/ bigger buffer
        Marshal.FreeHGlobal(infoPtr)
    End Try
    End Sub
TODO - a short description5/4/2008 4:16:28 AM - Jozef Izso-78.99.185.152An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29
```
