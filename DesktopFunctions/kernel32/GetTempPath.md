
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint GetTempPath(uint nBufferLength,
   [Out] StringBuilder lpBuffer);
```

## VB Signature:
```cs
Declare Function GetTempPath Lib "kernel32.dll" (nBufferLength As Integer, _
   <Out> lpBuffer As StringBuilder) As Integer
```

## Sample Code:
```cs
'TempFile.vb
'(DllImport declarations omitted)
Public Class TempFile
     Public Function Create(ByVal astrFoldername As String, _
                ByVal astrPrefix As String) As String
     Dim tempPath As New StringBuilder(MAX_PATH - 14)
     Dim tempName As New StringBuilder(MAX_PATH)
     Dim lngRet As Integer
     Dim result As String = ""

     lngRet = 1

     If (astrFoldername = "") Then
         lngRet = GetTempPath(MAX_PATH - 14, tempPath)
         astrFoldername = tempPath.ToString
     End If

     If (lngRet > 0 And lngRet <= MAX_PATH - 14) Then
         lngRet = GetTempFileName(astrFoldername, astrPrefix, 0, tempName)
         If lngRet <> 0 Then
         result = tempName.ToString
         End If
     End If

     Return result
   End Function

End Class
```

## Sample Code:
```cs
'This project references Microsoft.VisualStudio.QualityTools.UnitTestFramework
'TempFileTest.vb
Imports System.IO
Imports System.Text

Imports Microsoft.VisualStudio.TestTools.UnitTesting

'''<summary>
'''This is a test class for TempFileTest and is intended
'''to contain all TempFileTest Unit Tests
'''</summary>
<TestClass()> _
Public Class TempFileTest
    Private fFoldername As String = "C:\TempFile"
    Private fPrefix As String = "Prefix"  ' Only first three characters will be used by Windows API
    Private testContextInstance As TestContext

    '''<summary>
    '''Gets or sets the test context which provides
    '''information about and functionality for the current test run.
    '''</summary>
    Public Property TestContext() As TestContext
    Get
        Return testContextInstance
    End Get
    Set(ByVal value As TestContext)
        testContextInstance = value
    End Set
    End Property
```

## Sample Code:
```cs
'''<summary>
    '''A test for Create
    '''</summary>
    <TestMethod()> _
    Public Sub CreateTest()
    Dim target As TempFile = New TempFile
    Dim expected As String = fFoldername + "\" + Left(fPrefix, 3)  'Only part of the expected answer. The other part is random.
    Dim actual As String
    Dim dirInfo As DirectoryInfo

    If Not Directory.Exists(fFoldername) Then
        dirInfo = Directory.CreateDirectory(fFoldername)
        If Not dirInfo.Exists Then
        Throw New Exception("Directory '" + fFoldername + "' can not be created")
        End If
    End If

    actual = target.Create(fFoldername, fPrefix)
    Assert.IsTrue(File.Exists(actual))
    'Remove file before procedure exits.
    File.Delete(actual)
    Assert.AreEqual(Left(expected, Len(fFoldername) + 4), Left(actual, Len(fFoldername) + 4))

    Dim shortPath As New StringBuilder(TempFile.MAX_PATH)
    TempFile.GetShortPathName(Path.GetTempPath, shortPath, TempFile.MAX_PATH)
    expected = shortPath.ToString + Left(fPrefix, 3) ' GetTempPath end with "\"
    actual = target.Create("", fPrefix)
    Assert.IsTrue(File.Exists(actual))
    'Remove file before procedure exits.
    File.Delete(actual)
    Assert.AreEqual(Left(expected, Len(fFoldername) + 4), Left(actual, Len(fFoldername) + 4))
    End Sub
End Class
```
