
## C# Signature:
```cs
[DllImport("userenv.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool GetUserProfileDirectory(IntPtr hToken, StringBuilder path, ref int dwSize);
```

## Sample Code:
```cs
[DllImport("userenv.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool GetUserProfileDirectory(IntPtr hToken, StringBuilder path, ref int dwSize);

string GetUserProfilePath(IntPtr hToken)
{
    // get size of profile path string
    int dwSize = 0;
    GetUserProfileDirectory(hToken, null, ref dwSize);

    // get profile path of user
    StringBuilder profilePath = new StringBuilder(dwSize);
    if (!GetUserProfileDirectory(hToken, profilePath, ref dwSize))
    { // could not retrieve profile directory
        Console.Error.WriteLine("Cannot retrieve profile path. Error: " + Marshal.GetLastWin32Error().ToString());
        return "";
    }

    return profilePath.ToString();        
}
```
