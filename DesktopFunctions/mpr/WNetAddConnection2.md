
## C# Signatures:
```cs
// This must be used if NETRESOURCE is defined as a struct
[DllImport("mpr.dll")]    
public static extern int WNetAddConnection2(ref NETRESOURCE netResource,
   string password, string username, uint flags);

// This must be used if NETRESOURCE is defined as a class
[DllImport("mpr.dll")]    
public static extern int WNetAddConnection2(NETRESOURCE netResource,
   string password, string username, uint flags);

// by cozmo, it only worked for me this way; .NET 1.1, 11.01.2006
// dont know, what [In] means (some CAST ?), found it in microsoft.public.de.german.entwickler.dotnet.csharp
// my NETRESOURCE is defined as:
// [StructLayout(LayoutKind.Sequential)]
//    class NETRESOURCE
//    {    
//        public int dwScope;
//        etc...
//    }

  //by DaManu

  //
  //      public enum ResourceScope
  //      {
  //      RESOURCE_CONNECTED = 1,
  //      RESOURCE_GLOBALNET,
  //      RESOURCE_REMEMBERED,
  //      RESOURCE_RECENT,
  //      RESOURCE_CONTEXT
  //      };

  //      public enum ResourceType
  //      {
  //      RESOURCETYPE_ANY    = 0,
  //      RESOURCETYPE_DISK       = 1,
  //      RESOURCETYPE_PRINT      = 2,
  //      RESOURCETYPE_RESERVED   = 8,
  //      RESOURCETYPE_UNKNOWN    = -1,
  //      };

  //      public enum ResourceUsage
  //      {
  //      RESOURCEUSAGE_CONNECTABLE = 0x00000001,
  //      RESOURCEUSAGE_CONTAINER = 0x00000002,
  //      RESOURCEUSAGE_NOLOCALDEVICE = 0x00000004,
  //      RESOURCEUSAGE_SIBLING = 0x00000008,
  //      RESOURCEUSAGE_ATTACHED = 0x00000010,
  //      RESOURCEUSAGE_ALL = (RESOURCEUSAGE_CONNECTABLE | RESOURCEUSAGE_CONTAINER | RESOURCEUSAGE_ATTACHED),
  //      };

  //      public enum ResourceDisplayType
  //      {
  //      RESOURCEDISPLAYTYPE_GENERIC,
  //      RESOURCEDISPLAYTYPE_DOMAIN,
  //      RESOURCEDISPLAYTYPE_SERVER,
  //      RESOURCEDISPLAYTYPE_SHARE,
  //      RESOURCEDISPLAYTYPE_FILE,
  //      RESOURCEDISPLAYTYPE_GROUP,
  //      RESOURCEDISPLAYTYPE_NETWORK,
  //      RESOURCEDISPLAYTYPE_ROOT,
  //      RESOURCEDISPLAYTYPE_SHAREADMIN,
  //      RESOURCEDISPLAYTYPE_DIRECTORY,
  //      RESOURCEDISPLAYTYPE_TREE,
  //      RESOURCEDISPLAYTYPE_NDSCONTAINER
  //      };

  //      [StructLayout(LayoutKind.Sequential)]
  //      private class NETRESOURCE
  //      {
  //      public ResourceScope dwScope = 0;
  //      public ResourceType dwType = 0;
  //      public ResourceDisplayType dwDisplayType = 0;
  //      public ResourceUsage dwUsage = 0;
  //      public string lpLocalName = null;
  //      public string lpRemoteName = null;
  //      public string lpComment = null;
  //      public string lpProvider = null;
  //      };

  //
  //    [DllImport("Mpr.dll", EntryPoint="WNetAddConnection2", CallingConvention=CallingConvention.Winapi)]
  //      private static extern ErrorCodes WNetAddConnection2(NETRESOURCE lpNetResource,ref string lpPassword,ref 
  //                              string lpUsername, System.UInt32 dwFlags );
```

## C# Signatures:
```cs
[DllImport("mpr.dll")]    
public static extern int WNetAddConnection2( [In] NETRESOURCE netResource,
   string password, string username, int flags);
```

## VB Signatures:
```cs
' This must be used if NETRESOURCE is defined as a struct
Declare Function WNetAddConnection2 Lib "mpr.dll" (ByRef netResource As _
   NETRESOURCE, password As String, Username As String, Flag As Integer) As Integer

' This must be used if NETRESOURCE is defined as a class
Declare Function WNetAddConnection2 Lib "mpr.dll" (netResource As _
   NETRESOURCE, password As String, Username As String, Flag As Integer) As Integer
```

## Tips & Tricks:
```cs
using System.Runtime.InteropServices;
```

## Sample Code:
```cs
NETRESOURCE myNetResource = new NETRESOURCE();        
myNetResource.dwScope = 2;                    
myNetResource.dwType = 1 ;                    
myNetResource.dwDisplayType = 3;            
myNetResource.dwUsage = 1;            
myNetResource.LocalName = "z:";        
myNetResource.RemoteName = @"\servername\sharename";        
myNetResource.Provider = null;
```

## Sample Code:
```cs
int ret = WNetAddConnection2( myNetResource, "password", "username", 0); //by honglinlee

/*
  * if username = null the function uses the default user name
  *    (The user context for the process provides the default user name)
  * if password = null the function uses the current default password 
  *    associated with the user specified by the username parameter
  * if password = "" the function does not use a password
  */
```

## Sample Code:
```cs
public class NetworkConnection : IDisposable
  {
    string _networkName;

    public NetworkConnection(string networkName, 
    NetworkCredential credentials)
    {
    _networkName = networkName;

    var netResource = new NetResource()
    {
        Scope = ResourceScope.GlobalNetwork,
        ResourceType = ResourceType.Disk,
        DisplayType = ResourceDisplaytype.Share,
        RemoteName = networkName
    };

    var result = WNetAddConnection2(
        netResource, 
        credentials.Password,
        credentials.UserName,
        0);

    if (result != 0)
    {
        throw new IOException("Error connecting to remote share", 
        result);
    }   
    }

    ~NetworkConnection()
    {
    Dispose(false);
    }

    public void Dispose()
    {
    Dispose(true);
    GC.SuppressFinalize(this);
    }

    protected virtual void Dispose(bool disposing)
    {
    WNetCancelConnection2(_networkName, 0, true);
    }

    [DllImport("mpr.dll")]
    private static extern int WNetAddConnection2(NetResource netResource, 
    string password, string username, int flags);

    [DllImport("mpr.dll")]
    private static extern int WNetCancelConnection2(string name, int flags,
    bool force);
  }
```

## Sample Code:
```cs
public ResourceScope Scope;
    public ResourceType ResourceType;
    public ResourceDisplaytype DisplayType;
    public int Usage;
    public string LocalName;
    public string RemoteName;
    public string Comment;
    public string Provider;
```

## Sample Code:
```cs
Connected = 1,
    GlobalNetwork,
    Remembered,
    Recent,
    Context
```

## Sample Code:
```cs
Any = 0,
    Disk = 1,
    Print = 2,
    Reserved = 8,
```

## Sample Code:
```cs
Generic = 0x0,
    Domain = 0x01,
    Server = 0x02,
    Share = 0x03,
    File = 0x04,
    Group = 0x05,
    Network = 0x06,
    Root = 0x07,
    Shareadmin = 0x08,
    Directory = 0x09,
    Tree = 0x0a,
    Ndscontainer = 0x0b
```

## Sample Code:
```cs
//start copy/paste
using System.Runtime.InteropServices;

namespace Utilities.Network
{   
    public class NetworkDrive
    {
    public enum ResourceScope
    {
        RESOURCE_CONNECTED = 1,
        RESOURCE_GLOBALNET,
        RESOURCE_REMEMBERED,
        RESOURCE_RECENT,
        RESOURCE_CONTEXT
    }

    public enum ResourceType
    {
        RESOURCETYPE_ANY,
        RESOURCETYPE_DISK,
        RESOURCETYPE_PRINT,
        RESOURCETYPE_RESERVED
    }

    public enum ResourceUsage
    {
        RESOURCEUSAGE_CONNECTABLE = 0x00000001,
        RESOURCEUSAGE_CONTAINER = 0x00000002,
        RESOURCEUSAGE_NOLOCALDEVICE = 0x00000004,
        RESOURCEUSAGE_SIBLING = 0x00000008,
        RESOURCEUSAGE_ATTACHED = 0x00000010,
        RESOURCEUSAGE_ALL = (RESOURCEUSAGE_CONNECTABLE | RESOURCEUSAGE_CONTAINER | RESOURCEUSAGE_ATTACHED),
    }

    public enum ResourceDisplayType
    {
        RESOURCEDISPLAYTYPE_GENERIC,
        RESOURCEDISPLAYTYPE_DOMAIN,
        RESOURCEDISPLAYTYPE_SERVER,
        RESOURCEDISPLAYTYPE_SHARE,
        RESOURCEDISPLAYTYPE_FILE,
        RESOURCEDISPLAYTYPE_GROUP,
        RESOURCEDISPLAYTYPE_NETWORK,
        RESOURCEDISPLAYTYPE_ROOT,
        RESOURCEDISPLAYTYPE_SHAREADMIN,
        RESOURCEDISPLAYTYPE_DIRECTORY,
        RESOURCEDISPLAYTYPE_TREE,
        RESOURCEDISPLAYTYPE_NDSCONTAINER
    }

    [StructLayout(LayoutKind.Sequential)]
    private class NETRESOURCE
    {
        public ResourceScope dwScope = 0;
        public ResourceType dwType = 0;
        public ResourceDisplayType dwDisplayType = 0;
        public ResourceUsage dwUsage = 0;
        public string lpLocalName = null;
        public string lpRemoteName = null;
        public string lpComment = null;
        public string lpProvider = null;
    }

    [DllImport("mpr.dll")]
    private static extern int WNetAddConnection2(NETRESOURCE lpNetResource, string lpPassword, string lpUsername, int dwFlags);

    public int MapNetworkDrive(string unc, string drive, string user, string password)
    {
        NETRESOURCE myNetResource = new NETRESOURCE();
        myNetResource.lpLocalName = drive;
        myNetResource.lpRemoteName = unc;
        myNetResource.lpProvider = null;
        int result = WNetAddConnection2(myNetResource, password, user, 0);
        return result;
    }
    }
}
//end copy/paste
```

## Implimentation of C# Sample 3
```cs
Utilities.Network.NetworkDrive nd = new Utilities.Network.NetworkDrive();
if( nd.MapNetworkDrive(@"\\servername\shardrive","Z:",null,null) == 0 ) 
{
      Console.WriteLine("Mapped!");
}
else
{
    Console.WriteLine("Failed!");
}
```

## Implimentation of C# Sample 3
```cs
Public Function ConnectDrive(ByVal RemoteName As String, ByVal LocalName As String, Optional ByVal username As String = Nothing, Optional ByVal password As String = Nothing)
    Dim myResource As NETRESOURCE
    myResource.dwScope = 2
    myResource.dwType = 1
    myResource.dwDisplayType = 3
    myResource.LocalName = LocalName
    myResource.RemoteName = RemoteName
    myResource.dwUsage = Nothing
    myResource.Comment = Nothing
    myResource.Provider = Nothing
    Dim returnValue As Integer
    returnValue = WNetAddConnection2(myResource, password, username, 0)
    If returnValue <> 0 Then
        Dim errorM = New System.ComponentModel.Win32Exception(returnValue).Message
        MsgBox("Could not connect to " & myResource.RemoteName & ". The server said this: " & vbNewLine & vbNewLine & "(Error " & returnValue & ") " & errorM)
    End If

    Return returnValue
End Function
```
