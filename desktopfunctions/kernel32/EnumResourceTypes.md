
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool EnumResourceTypes(IntPtr hModule, EnumResTypeProc lpEnumFunc, IntPtr lParam);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
Private Shared Function EnumResourceTypes(ByVal hModule As IntPtr, ByVal lpEnumFunc As EnumResTypeProc, ByVal lParam As IntPtr) As Boolean
End Function
```

## Tips & Tricks:
```cs
''' <summary>
    ''' Enumerates a module for predefined resource types.
    ''' </summary>
    ''' <param name="fullPath">Address of a valid Win32 module.</param>
    ''' <param name="resources">If NULL, all resource types will be enumerated.</param>
    ''' <returns></returns>
    ''' <remarks></remarks>
    Public Shared Function GetResourceTypes(fullPath As String, _
                  resources() As ResourceType) As Dictionary(Of ResourceType,  _
                                               List(Of String))
    Dim hMod As IntPtr = LoadLibraryEx(fullPath, IntPtr.Zero, LoadLibraryFlags.LOAD_LIBRARY_AS_DATAFILE)
    If IntPtr.Zero.Equals(hMod) Then Return Nothing

    If IsNothing(resources) OrElse resources.Length = 0 Then resources = _
        CType([Enum].GetValues(GetType(ResourceType)), ResourceType())

    Dim LS As New Dictionary(Of ResourceType, List(Of String))

    Dim typeCallBack As New EnumResNameProcDelegate( _
         Function(hmodule As IntPtr, lpType As IntPtr, lpzName As IntPtr, lParam As IntPtr)
         Dim SLst As List(Of String) = Nothing
         Dim rt = CType(CInt(lpType), ResourceType)
         Dim ResID = MAKEINTRESOURCE(lpzName)
         If LS.TryGetValue(rt, SLst) Then
             SLst.Add(ResID)
         Else
             SLst = New List(Of String)({ResID})
             LS.Add(rt, SLst)
         End If
         Return True
         End Function)

    Dim callBack As New EnumResTypeProc( _
        Function(hm As IntPtr, rType As IntPtr, lp As IntPtr)
        Dim rt = CType(CInt(rType), ResourceType)
        If Array.IndexOf(resources, rt) > -1 Then
            EnumResourceNames(hm, rType, typeCallBack, IntPtr.Zero)
        End If
        Return True
        End Function)

    EnumResourceTypesW(hMod, callBack, IntPtr.Zero)
    FreeLibrary(hMod)
    Return LS
    End Function
```
