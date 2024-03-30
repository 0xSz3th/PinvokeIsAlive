
## C# Signature:
```cs
[DllImport("userenv.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern int CreateProfile( [MarshalAs(UnmanagedType.LPWStr)] String pszUserSid, [MarshalAs(UnmanagedType.LPWStr)] String pszUserName, [Out, MarshalAs(UnmanagedType.LPWStr)] System.Text.StringBuilder pszProfilePath, uint cchProfilePath);
```

## Sample Code:
```cs
using (System.Security.Principal.WindowsIdentity i = new System.Security.Principal.WindowsIdentity(token))
    {
        System.Text.StringBuilder s= new System.Text.StringBuilder(260);
        uint c= Convert.ToUInt32(s.Capacity);
        int hResult = CreateProfile(i.Owner.Value, username, s, c);
    }
```

## Sample PowerShell Code:
```cs
# Attempts to create a profile for the current logged on user.  Obviously, this will not work and it generates a return code 
    # of -2147024809.
    $TypeDefinition=@"
    [DllImport("userenv.dll", SetLastError = true, CharSet = CharSet.Auto)]
            public static extern int CreateProfile([MarshalAs(UnmanagedType.LPWStr)] String pszUserSid, [MarshalAs(UnmanagedType.LPWStr)] String pszUserName, [Out, MarshalAs(UnmanagedType.LPWStr)] System.Text.StringBuilder pszProfilePath, uint cchProfilePath);
    "@
    $u=Add-Type -MemberDefinition $TypeDefinition -Name "UserCreateProfile" -Namespace "UserProfile" -UsingNamespace "System.Security.Principal" -PassThru

    $token=[System.Security.Principal.WindowsIdentity]::GetCurrent().Token
    [System.Security.Principal.WindowsIdentity]$identity = new-object -TypeName System.Security.Principal.WindowsIdentity($token)
    #$identity.Owner.Value
    #$identity.Name

    $ProfilePath=""
    $intSizeOfProfilePath=0
    $u::CreateProfile($identity.Owner.Value, $identity.Name, $ProfilePath, $intSizeOfProfilePath)

    #$ProfilePath
    #$intSizeOfProfilePath
```

## Sample PowerShell to lookup Domain User / SID for CreateProfile
```cs
$userLogonDomain    = "YourDOMAIN"
    $userSamAccountName = "UserID"
    $domainAccount = $userLogonDomain + "\" + $userSamAccountName
    $strUserSid = ([System.Security.Principal.NTAccount] $domainAccount).Translate([System.Security.Principal.SecurityIdentifier]).Value
    #Create string buffer based on pszProfilePath's 260 char max (picking 240 char)
    $intSizeOfProfilePath = 240
    $ProfilePath = New-Object System.Text.StringBuilder($intSizeOfProfilePath)
    $u::CreateProfile($strUserSid, $userSamAccountName, $ProfilePath, $intSizeOfProfilePath)
Create a user profile directory structure in the profile's directory4/4/2016 6:12:07 PM - -66.192.63.2Create a user profile directory structure in the profile's directory4/4/2016 6:12:07 PM - -66.192.63.2
```
