
## C# Signature:
```cs
[DllImport("getuname.dll", SetLastError=true)]
static extern int GetUName(UInt16 wCharCode, [MarshalAs(UnmanagedType.LPWStr)] StringBuilder lpbuf);
```

## VB Signature:
```cs
Declare Function GetUName Lib "getuname.dll" (ByVal wCharCode As UShort, <MarshalAs(UnmanagedType.LPWStr)> ByVal lpbuf As StringBuilder) As Integer
```

## Sample C# Code:
```cs
var sb = new StringBuilder(256);
var len = GetUName('A', sb);
```

## Sample C# Code:
```cs
return sb.ToString(0, len);
```

## Sample VB Code:
```cs
Module UnicodeNative
     ''' <summary>Undocumented Win API function for getting localized character names</summary>
     ''' <param name="wCharCode">Character code (code-point)</param>
     ''' <param name="lpBuf">When function returns returns return value</param>
     ''' <returns>Number of characters returned</returns>
     Private Declare Function GetUName Lib "getuname.dll" (ByVal wCharCode As UShort, <MarshalAs(UnmanagedType.LPWStr)> ByVal lpbuf As System.Text.StringBuilder) As Integer
```

## Sample VB Code:
```cs
''' <summary>Gets localized name uf Unicode character</summary>
     ''' <param name="codePoint">Code point to get localizaed name of</param>
     ''' <returns>
     ''' Localized name of character represented by <paramref name="codePoint"/>. The name is localized to current system locale, not to current thread UI culture.
     ''' Returns null if <paramref name="codePoint"/> is not supported by Windows function for getting character names (i.e. <paramref name="codePoint"/> is greater than <see cref="UInt16.MaxValue"/>) or if name cannot be obtained or windows function call failed.
     ''' </returns>
     ''' <exception cref="ArgumentOutOfRangeException"><paramref name="codePoint"/> is greater than 0x10FFFF</exception>
     ''' <remarks>
     ''' <para>This function is not CLS-Compliant. CLS-compliant overload exists.</para>
     ''' <para>This function relies on undocumented Windows API <c>GetUName</c>. It is possible that this API will be changed or removed in future version of Windows and this function will become slow and start returning nullls for all calls. It can also possibly carsh your application or system. Use on own risk.</para>
     ''' </remarks>
     <CLSCompliant(False)>
     Public Function GetCharacterName(codePoint As UInteger) As String
     If codePoint > &H10FFFFUI Then Throw New ArgumentOutOfRangeException("codePoint")
     If codePoint > UShort.MaxValue Then Return Nothing

     Dim buff As New StringBuilder(1024)

     Dim ret%
     Try
         ret = API.Misc.GetUName(codePoint, buff)
     Catch
         Return Nothing
     End Try
     If ret <= 0 Then Return Nothing
     Return buff.ToString

     End Function
End Module
```
