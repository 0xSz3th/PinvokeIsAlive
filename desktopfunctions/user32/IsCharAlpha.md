
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool IsCharAlphaNumeric(char ch);
```

## Sample Code:
```cs
Option Explicit
```

## Sample Code:
```cs
strChar = Mid(strOrigString, lngCtr, 1)

    'Check if char is alphanumeric with userlib function
    If IsCharAlphaNumericW(AscW(strChar)) = 1 Then
    Mid(strNewString, lngCtr2, 1) = strChar
    lngCtr2 = lngCtr2 + 1
    Else
    'if not replace by a space
    Mid(strNewString, lngCtr2, 1) = " "
    lngCtr2 = lngCtr2 + 1

    End If
```

## Sample Code:
```cs
strNewString = Left(strNewString, lngCtr2 - 1)
```

## Sample Code:
```cs
strNewString = ""
```
