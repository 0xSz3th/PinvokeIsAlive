
## C# Signature:
```cs
[DllImport("mpr.dll", CharSet=CharSet.Auto, SetLastError=true)]
    public static extern int WNetGetConnection([MarshalAs(UnmanagedType.LPTStr)] string localName, [MarshalAs(UnmanagedType.LPTStr)] StringBuilder remoteName, ref int length);
```

## VB Signature:
```cs
''' <summary>
    ''' Use to get UNC Path of a Mapped Drive
    ''' </summary>
    ''' <param name="localName"></param>
    ''' <param name="remoteName"></param>
    ''' <param name="length"></param>
    ''' <returns></returns>
    ''' <remarks></remarks>
    <DllImport("mpr.dll")> _
    Shared Function WNetGetConnection(<MarshalAs(UnmanagedType.LPTStr)> _
                      ByVal localName As String, ByVal remoteName As System.Text.StringBuilder, _
                      ByRef length As Integer) As Integer
    End Function
```

## Alternative VB Signature:
```cs
Declare Function WNetGetConnection Lib "mpr.dll" Alias "WNetGetConnectionA" (ByVal localName As String, ByVal remoteName As System.Text.StringBuilder, ByRef length As Integer) As Integer
```

## Sample Code for Visal Basic 2005 Express Edition:
```cs
Declare Function WNetGetConnection Lib "mpr.dll" Alias "WNetGetConnectionA" (ByVal localName As String, _
    ByVal remoteName As System.Text.StringBuilder, ByRef length As Integer) As Integer

    Private Function strToUnc(ByVal path As String)
        Dim length As Integer = 255
        Dim UNC As New System.Text.StringBuilder(length)
        WNetGetConnection(Microsoft.VisualBasic.Left(path, 2), UNC, length)
        Return UNC.ToString
    End Function

    'to get the UNC-Path of a network-drive use something like:
    Private Sub Test()
        Dim dr As String = "J:\"
        MsgBox("The UNC-Path of drive " & dr & " is: " & strToUnc(dr))
    End Sub
```

## Sample Code for VB.NET with error handling:
```cs
Declare Function WNetGetConnection Lib "mpr.dll" Alias "WNetGetConnectionA" _
                      (ByVal localName As String, _
                      ByVal remoteName As System.Text.StringBuilder, _
                      ByRef length As Integer) As Integer

Private Sub DisplayUncPath(ByVal aLocalPath As String)

    Dim theDriveName As String = aLocalPath.Substring(0, aLocalPath.IndexOf(":") + 1)
    If theDriveName <> "" Then
        Dim theDriveInfo As New DriveInfo(theDriveName)
        If theDriveInfo.DriveType = DriveType.Network Then
        Dim uncPathBuf As New StringBuilder(259)
        Dim err As Integer = WNetGetConnection(theDriveName, uncPathBuf, uncPathBuf.Capacity)
        If err = 0 Then
            Dim pathname As String = uncPathBuf.ToString()
            MessageBox.Show(aLocalPath.Replace(theDriveName, pathname))
        Else
            MessageBox.Show("Failed with error :" & err)
        End If
        Else
        MessageBox.Show(theDriveName & " is not a network mapped path.")
        End If
      End If
End Sub
```
