
## C# Definition:
```cs
/// <summary>
/// Represents possible values returned by the MessageBox function.
/// </summary>
public enum MessageBoxResult : uint
{
    Ok = 1,
    Cancel=2,
    Abort=3,
    Retry=4,
    Ignore=5,
    Yes=6,
    No=7,
    Close=8,
    Help=9,
    TryAgain=10,
    Continue=11,
    Timeout = 32000
}
```

## VB.NET Definition:
```cs
''' <summary>
''' Represents possible values returned by the MessageBox function.
''' </summary>
Public Enum MessageBoxResult As UInteger
     Ok = 1
     Cancel
     Abort
     Retry
     Ignore
     Yes
     No
     Close
     Help
     TryAgain
     ContinueOn
     Timeout = 32000
End Enum
```

## VB Definition:
```cs
public Enum MessageBoxResult 
     Ok     As Long = 1
     Cancel     As Long = 2
     Abort      As Long = 3
     Retry      As Long = 4
     Ignore     As Long = 5
     Yes    As Long = 6
     No     As Long = 7
     Close      As Long = 8
     Help       As Long = 9
     TryAgain   As Long = 10
     ContinueOn As Long = 11
     Timeout    As Long = 32000
End Enum
```

## Managed API Alternative:
```cs
System.Windows.Forms.DialogResult
```
