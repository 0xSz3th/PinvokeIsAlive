
## C# Signature:
```cs
[DllImport("netapi32.dll", CharSet=CharSet.Unicode)]
static extern int NetJoinDomain(
          string lpServer,
          string lpDomain,
          string lpAccountOU,
          string lpAccount,
          string lpPassword,
          JoinOptions NameType);
```

## VB Signature:
```cs
Declare Unicode Function NetJoinDomain Lib "Netapi32.dll" _
        (ByVal lpServer As String, _
        ByVal lpDomain As String, _
        ByVal lpAccountOU As String, _
        ByVal lpAccount As String, _
        ByVal lpPassword As String, _
        ByVal fJoinOptions As Integer) As Integer
```

## User-Defined Types:
```cs
[Flags]
        public enum JoinOptions
        {
          NETSETUP_JOIN_DOMAIN = 0x00000001,
          NETSETUP_ACCT_CREATE = 0x00000002,
          NETSETUP_ACCT_DELETE = 0x00000004,
          NETSETUP_WIN9X_UPGRADE = 0x00000010,
          NETSETUP_DOMAIN_JOIN_IF_JOINED = 0x00000020,
          NETSETUP_JOIN_UNSECURE = 0x00000040,
          NETSETUP_MACHINE_PWD_PASSED = 0x00000080,
          NETSETUP_DEFER_SPN_SET = 0x00000100,
        }
```

## C# Sample:
```cs
public class join
    {

    [DllImport("netapi32.dll", CharSet = CharSet.Unicode)]
    static extern uint NetJoinDomain(
      string lpServer,
      string lpDomain,
      string lpAccountOU,
      string lpAccount,
      string lpPassword,
      JoinOptions NameType);

    [Flags]
    enum JoinOptions
    {
        NETSETUP_JOIN_DOMAIN = 0x00000001,
        NETSETUP_ACCT_CREATE = 0x00000002,
        NETSETUP_ACCT_DELETE = 0x00000004,
        NETSETUP_WIN9X_UPGRADE = 0x00000010,
        NETSETUP_DOMAIN_JOIN_IF_JOINED = 0x00000020,
        NETSETUP_JOIN_UNSECURE = 0x00000040,
        NETSETUP_MACHINE_PWD_PASSED = 0x00000080,
        NETSETUP_DEFER_SPN_SET = 0x10000000
    }

    public static uint domainjoin(string server, string domain, string OU, string account, string password)
    {
        try
        {
        uint value1 = NetJoinDomain(server, domain, OU, account, password, (JoinOptions.NETSETUP_JOIN_DOMAIN | JoinOptions.NETSETUP_DOMAIN_JOIN_IF_JOINED | JoinOptions.NETSETUP_ACCT_CREATE));
        return value1;
        }
        catch (Exception e)
        {
        MessageBox.Show(e.Message);
        return 11;
        }
    }
    }
```
