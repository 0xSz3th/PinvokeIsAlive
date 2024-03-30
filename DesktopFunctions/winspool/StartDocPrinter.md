
## C# Signature:
```cs
[DllImport("winspool.dll", SetLastError=true)]
static extern TODO StartDocPrinter(TODO);
```

## VB Signature:
```cs
Declare Function StartDocPrinter Lib "winspool.dll" (TODO) As TODO
```

## VB Signature:
```cs
<DllImport("winspool.drv", EntryPoint:="StartDocPrinterA", ExactSpelling:=True, SetLastError:=True, CallingConvention:=CallingConvention.StdCall, CharSet:=CharSet.Ansi)> _
Private Shared Function StartDocPrinter(ByVal hPrinter As IntPtr, ByVal level As Integer, ByRef pDocInfo As DOC_INFO_1) As Integer
End Function
```

## Sample Code:
```cs
Public Function StartDoc(hPrinter as IntPtr, ByVal documentTitle As String) As Boolean
        Dim di As New DOC_INFO_1
        With di
        .pDocName = documentTitle
        .pOutputFile = vbNullString
        .pDatatype = vbNullString
        End With
        Dim printJobID as Integer = StartDocPrinter(hPrinter, 1, di)
        Return (printJobID <> 0)
    End Function
```
