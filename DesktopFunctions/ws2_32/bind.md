[DllImport("Ws2_32.dll")]
    public static extern int bind(IntPtr s, ref sockaddr_in addr, int addrsize);
[DllImport("Ws2_32.dll")]
    public static extern int bind(IntPtr s, ref sockaddr_in6 addr, int addrsize);

## VB Signature:
```cs
Declare Function bind Lib "ws2_32.dll" ( _
        socketHandle As IntPtr, _
        ByRef socketAddress As sockaddr_in, _
        addressLength as Integer) As Integer
```

## User-Defined Types:
```cs
/// <summary>
/// Internet socket address structure.
/// </summary>
```

## Sample Code:
```cs
public static bool Bind(string ipAddress, int port, IntPtr socketHandle)
{
    sockaddr_in remoteAddress;            //Remote address structure.
    int resultCode = 0;            //Result of operation.
    int errorCode = 0;                //Resultant error.
    bool returnValue = false;            //Return value.

    if (socketHandle != IntPtr.Zero)
    {
        try
        {
            //Attempt to create the destination address.
            remoteAddress = new sockaddr_in();
            remoteAddress.sin_family = SocketsConstants.AF_INET;
            remoteAddress.sin_port = htons((short)port);
            remoteAddress.sin_addr = inet_addr(ipAddress);
            remoteAddress.sin_zero = 0;

            //Check to ensure the address translated correctly.
            if (remoteAddress.sin_addr != 0)
            {
                //Attempt to connect.
                resultCode = bind(socketHandle, ref remoteAddress, 
                    Marshal.SizeOf(remoteAddress));
                errorCode = Marshal.GetLastWin32Error();
                returnValue = (resultCode == 0);
            }
        }
        catch
        {
            returnValue = false;
        }
    }
    return returnValue;
}
```
