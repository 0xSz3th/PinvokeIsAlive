
## C# Signature:
```cs
[DllImport("shlwapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
    public static extern bool PathCanonicalize([Out] StringBuilder dst, string src);
```

## VB Signature:
```cs
Declare Function PathCanonicalize Lib "shlwapi.dll" Alias "PathCanonicalizeA" (ByVal lpszDest As String, ByVal lpszSrc As String) As Long
```

## User-Defined Types:
```cs
None.
```

## Alternative Managed API:
```cs
TODO. Path. ?
```

## Notes:
```cs
This function allows the user to specify what to remove from a path by inserting special character sequences into the path. The ".." sequence indicates to remove the path part from the current position to the previous path part. The "." sequence indicates to skip over the next path part to the following path part. The root part of the path cannot be removed.
```
