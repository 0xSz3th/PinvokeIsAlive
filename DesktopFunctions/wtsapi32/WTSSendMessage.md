
## C# Signature:
```cs
[DllImport("wtsapi32.dll", SetLastError=true)]
static extern bool WTSSendMessage(
            IntPtr hServer,
            [MarshalAs(UnmanagedType.I4)] int SessionId,
            String pTitle,
            [MarshalAs(UnmanagedType.U4)] int TitleLength,
            String pMessage, 
            [MarshalAs(UnmanagedType.U4)] int MessageLength,
            [MarshalAs(UnmanagedType.U4)] int Style,
            [MarshalAs(UnmanagedType.U4)] int Timeout,
            [MarshalAs(UnmanagedType.U4)] out int pResponse,
            bool bWait);
```

## VB Signature:
```cs
<DllImport("wtsapi32.dll", SetLastError:=True)> _
  Private Shared Function WTSSendMessage(ByVal hServer As IntPtr, ByVal SessionId As Int32, ByVal title As String, ByVal titleLength As UInt32, ByVal message As String, ByVal messageLength As UInt32, ByVal style As UInt32, ByVal timeout As UInt32, ByRef pResponse As UInt32, ByVal bWait As Boolean) As Boolean
  End Function
```

## PowerShell Signature:
```cs
[DllImport("wtsapi32.dll", SetLastError = true)]
    public static extern bool WTSSendMessage(
        IntPtr hServer,
        [MarshalAs(UnmanagedType.I4)] int SessionId,
        String pTitle,
        [MarshalAs(UnmanagedType.U4)] int TitleLength,
        String pMessage,
        [MarshalAs(UnmanagedType.U4)] int MessageLength,
        [MarshalAs(UnmanagedType.U4)] int Style,
        [MarshalAs(UnmanagedType.U4)] int Timeout,
        [MarshalAs(UnmanagedType.U4)] out int pResponse,
        bool bWait);
```

## Notes:
```cs
// Useful constants
    public static IntPtr WTS_CURRENT_SERVER_HANDLE = IntPtr.Zero;
    public static int WTS_CURRENT_SESSION = -1;
```

## Sample Code:
```cs
public static IntPtr WTS_CURRENT_SERVER_HANDLE = IntPtr.Zero;
    public static int WTS_CURRENT_SESSION = -1;

    bool result = false;
    String title = "Hello";
    int tlen = title.Length;
    String msg = "Terminal Service!";
    int mlen = msg.Length;
    int resp = 0;
    result = WTSSendMessage(WTS_CURRENT_SERVER_HANDLE, WTS_CURRENT_SESSION, title, tlen, msg, mlen, 0, 0, out resp, false);
    int err = Marshal.GetLastWin32Error();
    System.Console.WriteLine("result:{0}, errorCode:{1}, response:{2}", result, err, resp);
```

##  PowerShell Example
```cs
#http://technet.microsoft.com/en-us/query/aa383842
    #http://technet.microsoft.com/en-us/query/aa383488
    Function Send-TSMessageBox
    {
        param([int]$sessionId = 1, [string]$title = "Title", [string]$message = "Message", [int]$buttonSet = 4, [int]$timeout = 0, [bool]$waitResponse = $false)

            $signature = @"
            [DllImport("wtsapi32.dll", SetLastError = true)]
            public static extern bool WTSSendMessage(
                IntPtr hServer,
                [MarshalAs(UnmanagedType.I4)] int SessionId,
                String pTitle,
                [MarshalAs(UnmanagedType.U4)] int TitleLength,
                String pMessage,
                [MarshalAs(UnmanagedType.U4)] int MessageLength,
                [MarshalAs(UnmanagedType.U4)] int Style,
                [MarshalAs(UnmanagedType.U4)] int Timeout,
                [MarshalAs(UnmanagedType.U4)] out int pResponse,
                bool bWait);
    "@

                [int]$titleLength = $title.Length;
                [int]$messagelength = $message.Length;
                [int]$response = 0;

                $MessageBox = Add-Type -memberDefinition $signature -name "WTSAPISendMessage" -namespace WTSAPI -passThru   
                $MessageBox::WTSSendMessage(0, $sessionId, $title, $titleLength, $message, $messageLength, $buttonSet, $timeout, [ref] $response, $waitResponse)

                $response
    }

    #ABORT 3
    #CANCEL 2
    #IGNORE 5
    #NO 7
    #OK 1
    #RETRY 4
    #YES 6
    #ASYNC 32001 (0x7D01)
    #The bWait parameter was FALSE, so the function returned without waiting for a response.
    #TIMEOUT 32000 (0x7D00)
    #The bWait parameter was TRUE and the time-out interval elapsed.
```
