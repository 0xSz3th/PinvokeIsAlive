
## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError = true, CharSet = CharSet.Auto)]
   static extern IntPtr FtpFindFirstFile(IntPtr hConnect,
   string searchFile, out WIN32_FIND_DATA findFileData,
   int flags, IntPtr context);
```

## VB Signature:
```cs
Declare Function FtpFindFirstFile Lib "wininet.dll" _
   (ByVal hConnect As IntPtr, ByVal searchFile As String, _
   ByRef findFileData As WIN32_FIND_DATA, ByVal flags As Integer, _
   ByVal context As IntPtr) As IntPtr
```

## Sample Code:
```cs
Do
        '
        bRet = InternetFindNextFile(hFind, pData)
```

## Sample Code:
```cs
If Not bRet Then
          Procces the error here and quit
        Else        
        Pos = InStr(pData.cFileName, " ") ' The file name should be at the start of the line
        If Pos > 0 Then
            strItemName = Trim(Left(pData.cFileName, Pos)) ' Get the file name
        End If
        ' Add the name to a list - Could be a list box as below or Text box 
        Form1.List_Files.Items.Add(strItemName)
    Loop
    '
    InternetCloseHandle(hFind) ' close the handle.
    End Sub
```
