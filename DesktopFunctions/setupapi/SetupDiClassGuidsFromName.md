
## C# Signature:
```cs
[DllImport("setupapi.dll", SetLastError=true)]
static extern bool SetupDiClassGuidsFromName(string ClassName, ref Guid ClassGuidArray1stItem, UInt32 ClassGuidArraySize, out UInt32 RequiredSize);
```

## VB Signature:
```cs
<DllImport("setupapi.dll")> _
    Private Shared Function SetupDiClassGuidsFromName( _
    ByVal ClassName As StringBuilder, _
    ByRef ClassGuids As Guid, _
    ByVal ClassGuidSize As Integer, _
    ByRef ClassGuidRequiredSize As Integer) As Boolean
    End Function
```

## Notes:
```cs
C# signature works.
```

##  C# Sample Code:
```cs
UInt32 RequiredSize = 0;
    Guid[] GuidArray = new Guid[1];
    // read Guids
    bool Status = SetupDiClassGuidsFromName("class name here", ref GuidArray[0], 1, out RequiredSize);
    if (true == Status)
    {
            if (1 < RequiredSize)
        {
        GuidArray = new Guid[RequiredSize];
        SetupDiClassGuidsFromName("class name here", ref GuidArray[0], RequiredSize, out RequiredSize);
        }
    }
    else
    {
        UInt32 ErrorCode;
        ErrorCode = GetLastError();
    }
```

##  VB.Net Sample Code:
```cs
Dim ClassName As New StringBuilder("net")
    Dim ClassGuid As Guid
    Dim GuidSize As Integer = 0
    Dim GuidReqtSize As Integer
    Dim intRtrn As Integer
    intRtrn = SetupDiClassGuidsFromName(ClassName, ClassGuid, GuidSize, GuidReqtSize)
    GuidSize = GuidReqtSize
    intRtrn = SetupDiClassGuidsFromName(ClassName, ClassGuid, GuidSize, GuidReqtSize)
    MsgBox(ClassGuid.ToString)
```
