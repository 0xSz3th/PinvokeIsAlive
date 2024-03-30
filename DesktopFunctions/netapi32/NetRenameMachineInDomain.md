
## C# Signature:
```cs
[DllImport("netapi32.dll", SetLastError=true, CharSet = CharSet.Unicode)]
    internal static extern int NetRenameMachineInDomain(
        string lpServer,
        string lpNewMachineName,
        string lpAccount,
        string lpPassword,
        uint fRenameOptions
        );
```

## VB Signature:
```cs
Declare Function NetRenameMachineInDomain Lib "netapi32.dll" (TODO) As TODO
```

## C# User-Defined Types:
```cs
internal const uint NETSETUP_ACCT_CREATE = 2;
```

## C# Sample Code:
```cs
[DllImport("netapi32.dll", SetLastError=true, CharSet = CharSet.Unicode)]
    internal static extern int NetRenameMachineInDomain(
        string lpServer,
        string lpNewMachineName,
        string lpAccount,
        string lpPassword,
        uint fRenameOptions
        );

    internal const uint NETSETUP_ACCT_CREATE = 2;

    private string _domainUser = @"domain\domainuser";
    private string _domainPassword = "domainpassword";

    private void RenameMachine()
    {
        //This function will change the current PC's name to "PCNEWNAME" using the given domain account.  This changes it both locally and on the domain.

        int error = 0;
        error = NetRenameMachineInDomain(null, "PCNEWNAME", _domainUser, _domainPassword, NETSETUP_ACCT_CREATE);

        if(error == 0)
        {
            MessageBox.Show("Rename Successful.");
        }
        else
        {
            MessageBox.Show("Rename Failed.\r\nError: " + error.ToString());
        }
    }
```
