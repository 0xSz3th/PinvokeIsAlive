
## C# Signature:
```cs
[DllImport("credui.dll", EntryPoint="CredUIParseUserNameW", CharSet=CharSet.Unicode)]
private static extern CredUIReturnCodes CredUIParseUserName(
        string userName,
        StringBuilder user,
        int userMaxChars,
        StringBuilder domain,
        int domainMaxChars);
```

## VB Signature:
```cs
TODO
```

## Sample Code:
```cs
/// <summary>
/// Extracts the domain and user account name from a fully qualified user name.
/// </summary>
/// <param name="userName">A <see cref="string"/> that contains the user name to be parsed. The name must be in UPN or down-level format, or a certificate.</param>
/// <param name="user">A <see cref="string"/> that receives the user account name.</param>
/// <param name="domain">A <see cref="string"/> that receives the domain name. If <paramref name="userName"/> specifies a certificate, pszDomain will be <see langword="null"/>.</param>
/// <returns>
///     <see langword="true"/> if the <paramref name="userName"/> contains a domain and a user-name; otherwise, <see langword="false"/>.
/// </returns>
[System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1021:AvoidOutParameters")]
public static bool ParseUserName(string userName, out string user, out string domain)
{
    if (string.IsNullOrEmpty(userName))
    throw new ArgumentNullException("userName");

    StringBuilder userBuilder = new StringBuilder();
    StringBuilder domainBuilder = new StringBuilder();

    CredUIReturnCodes returnCode = NativeMethods.CredUIParseUserName(userName, userBuilder, int.MaxValue, domainBuilder, int.MaxValue);
    switch (returnCode)
    {
    case CredUIReturnCodes.NO_ERROR: // The username is valid.
        user = userBuilder.ToString();
        domain = domainBuilder.ToString();
        return true;

    case CredUIReturnCodes.ERROR_INVALID_ACCOUNT_NAME: // The username is not valid.
        user = userName;
        domain = null;
        return false;

    // Impossible to reach this state
    //case CredUIReturnCodes.ERROR_INSUFFICIENT_BUFFER: // One of the buffers is too small.
    //    throw new OutOfMemoryException();

    case CredUIReturnCodes.ERROR_INVALID_PARAMETER: // ulUserMaxChars or ulDomainMaxChars is zero OR userName, user, or domain is NULL.
        throw new ArgumentNullException("userName");

    default:
        user = null;
        domain = null;
        return false;
    }
}
```
