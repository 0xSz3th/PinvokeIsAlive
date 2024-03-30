
## C# Signature:
```cs
[DllImport("oleaut32.dll", EntryPoint = "UnRegisterTypeLib", CharSet = CharSet.Auto, SetLastError = true)]
    private static extern int UnRegisterTypeLib(
        ref Guid libID,
        short wVerMajor,
        short wVerMinor,
        int lCID,
        SYSKIND tSysKind);
```

## VB.Net Signatures:
```cs
Declare Unicode Function UnRegisterTypeLib Lib "oleaut32.dll" (ByRef LibID As System.Guid, ByVal nVerMajor As Short, ByVal nVerMinor As Short, ByVal lCID As Integer, ByVal tSysKind As System.Runtime.InteropServices.ComTypes.SYSKIND) As Integer
```

## VB 6 Signature:
```cs
Declare Function UnRegisterTypeLib Lib "oleaut32.dll" (LibID As tGUID, ByVal nVerMajor As Integer, ByVal nVerMinor As Integer, ByVal lCID As Long, ByVal tSysKind As eSYSKIND) As Long
```

## User-Defined Types:
```cs
'VB6
Type tGUID
    Data1 As Long
    Data2 As Integer
    Data3 As Integer
    Data4(0 To 7) As Byte
End Type

Enum eSYSKIND
    SYS_WIN16 = 0&
    SYS_WIN32 = 1&
    SYS_MAC = 2&
    SYS_WIN64 = 3&
End Enum
```

## Sample Code:
```cs
'VB.Net  Register or Unregister a Type Library file
    Private Declare Unicode Function LoadTypeLib Lib "oleaut32.dll" (ByVal TLpszModule As String, ByRef TPpTypeLib As ComTypes.ITypeLib2) As Integer
    Private Declare Unicode Function RegisterTypeLib Lib "oleaut32.dll" (ByVal ptlib As ComTypes.ITypeLib2, ByVal szFullPath As String, ByVal szHelpDir As String) As Integer
    Private Declare Unicode Function UnRegisterTypeLib Lib "oleaut32.dll" (ByRef LibID As System.Guid, ByVal nVerMajor As Short, ByVal nVerMinor As Short, ByVal lCID As Integer, ByVal tSysKind As ComTypes.SYSKIND) As Integer

    Private Const ERROR_SUCCESS As Short = 0

    Public Function RegisterTLib(ByVal strFile As String, ByVal bRegister As Boolean) As Boolean
        Dim nResult As Integer
        Dim TLB As ComTypes.ITypeLib2 = Nothing
        Dim tlbAttrPtr As IntPtr
        Dim tlbAttr As ComTypes.TYPELIBATTR

        On Error Resume Next

        If My.Computer.FileSystem.FileExists(strFile) = False Then
            RegisterTLib = False
        Else
            nResult = LoadTypeLib(strFile, TLB)

            If nResult = ERROR_SUCCESS Then
                If bRegister Then
                    nResult = RegisterTypeLib(TLB, strFile, Nothing)

                    If nResult = ERROR_SUCCESS Then 'success
                        RegisterTLib = true
                    Else 'failure
                        RegisterTLib = False
                    End If
                Else
                    TLB.GetLibAttr(tlbAttrPtr)
                    tlbAttr = CType(Marshal.PtrToStructure(tlbAttrPtr, GetType(ComTypes.TYPELIBATTR)), ComTypes.TYPELIBATTR)

                    nResult = UnRegisterTypeLib(tlbAttr.guid, tlbAttr.wMajorVerNum, tlbAttr.wMinorVerNum, tlbAttr.lcid, tlbAttr.syskind)
                    tlbAttr = Nothing
                    TLB.ReleaseTLibAttr(tlbAttrPtr)

                    If nResult = ERROR_SUCCESS Then 'success
                        RegisterTLib = True
                    Else 'failure
                        RegisterTLib = False
                    End If
                End If
            Else ' error loading the TypeLibrary file
                RegisterTLib = False
            End If
        End If
    End Function
```
