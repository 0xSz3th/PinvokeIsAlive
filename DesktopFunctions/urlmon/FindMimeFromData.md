
## C# Signature:
```cs
[DllImport("urlmon.dll", CharSet = CharSet.Unicode, ExactSpelling = true, SetLastError = false)]
    static extern int FindMimeFromData(IntPtr pBC,
          [MarshalAs(UnmanagedType.LPWStr)] string pwzUrl,
         [MarshalAs(UnmanagedType.LPArray, ArraySubType=UnmanagedType.I1, SizeParamIndex=3)] 
        byte[] pBuffer,
          int cbSize,
             [MarshalAs(UnmanagedType.LPWStr)]  string pwzMimeProposed,
          int dwMimeFlags,
          out IntPtr ppwzMimeOut,
          int dwReserved);
```

## VB.NET Signature:
```cs
''' <summary>No flags specified. Use default behavior for the function.</summary>
    [Default] = &H0
    ''' <summary>Treat the specified pwzUrl as a file name. </summary>
    URLAsFileName = &H1
    ''' <summary>Internet Explorer 6 for Windows XP SP2 and later. Use MIME-type detection even if FEATURE_MIME_SNIFFING is detected. Usually, this feature control key would disable MIME-type detection.</summary>
    EnableMIMESniffing = &H2
    ''' <summary>Internet Explorer 6 for Windows XP SP2 and later. Perform MIME-type detection if "text/plain" is proposed, even if data sniffing is otherwise disabled. Plain text may be converted to text/html if HTML tags are detected. </summary>
    IgnoreMIMETextPlain = &H4
    ''' <summary>Internet Explorer 8. Use the authoritative MIME type specified in pwzMimeProposed. Unless <see cref="MIMEFlags.IgnoreMIMETextPlain "/> is specified, no data sniffing is performed.</summary>
    ServerMIME = &H8
    ''' <summary>Internet Explorer 9. Do not perform detection if "text/plain" is specified in pwzMimeProposed.</summary>
    RespectTextPlain = &H10
    ''' <summary>Internet Explorer 9. Returns image/png and image/jpeg instead of image/x-png and image/pjpeg. </summary>
    ReturnUpdatedImgMIMEs = &H20
```

## VB.NET Signature:
```cs
<DllImport("urlmon.dll", CharSet:=CharSet.Auto)> _
    Private Shared Function FindMimeFromData( _
        ByVal pBC As IntPtr, _
        <MarshalAs(UnmanagedType.LPWStr)> _
        ByVal pwzUrl As String, _
        <MarshalAs(UnmanagedType.LPArray, ArraySubType:=UnmanagedType.I1, SizeParamIndex:=3)> ByVal _
        pBuffer As Byte(), _
        ByVal cbSize As Integer, _
        <MarshalAs(UnmanagedType.LPWStr)> _
        ByVal pwzMimeProposed As String, _
        ByVal dwMimeFlags As Integer, _
        <MarshalAs(UnmanagedType.LPWStr)> _
        ByRef ppwzMimeOut As String, _
        ByVal dwReserved As Integer) As Integer
    End Function
```

## VB Signature:
```cs
Public Declare Function FindMimeFromData Lib "urlmon.dll" ( _
        ByVal pbc As Long, _
        ByVal pwzUrl As String, _
        pBuffer As Any, _
        cbSize As Long, _
        ByVal pwzMimeProposed As String, _
        dwMimeFlags As Long, _
        ppwzMimeOut As Long, _
        dwReserved As Long) As Long
```

## Notes:
```cs
'Convert a LPWSTR pointer to a VB string
    Private Function PtrToString(lpwString As Long) As String
        Dim Buffer() As Byte
        Dim nLen As Long

        If lpwString Then
        nLen = lstrlenW(lpwString) * 2
        If nLen Then
            ReDim Buffer(0 To (nLen - 1)) As Byte
                CopyMemory Buffer(0), ByVal lpwString, nLen
            PtrToString = Buffer
        End If
        End If
    End Function
```

## Sample Code:
```cs
public string MimeTypeFrom(byte[] dataBytes, string mimeProposed) {
   if (dataBytes == null)
     throw new ArgumentNullException("dataBytes");
   string mimeRet = String.Empty;
   IntPtr suggestPtr = IntPtr.Zero, filePtr = IntPtr.Zero, outPtr = IntPtr.Zero;
   if (mimeProposed != null && mimeProposed.Length > 0) {
     //suggestPtr = Marshal.StringToCoTaskMemUni(mimeProposed); // for your experiments ;-)
     mimeRet = mimeProposed;
   }
   int ret = FindMimeFromData(IntPtr.Zero, null, dataBytes, dataBytes.Length, mimeProposed, 0, out outPtr, 0);
   if (ret == 0 && outPtr != IntPtr.Zero) {
     mimeRet = Marshal.PtrToStringUni(outPtr);
     Marshal.FreeCoTaskMem(outPtr); //msdn docs wrongly states that operator 'delete' must be used. Do not remove FreeCoTaskMem
     return mimeRet;

   }
   return mimeRet;
}

// call it this way:
Trace.Write("MimeType is " + MimeTypeFrom(Encoding.ASCII.GetBytes("%PDF-"), "text/plain"));
```

## Alternative Managed API:
```cs
/// <summary>
    /// Ensures that file exists and retrieves the content type 
    /// </summary>
    /// <param name="file"></param>
    /// <returns>Returns for instance "images/jpeg" </returns>
    public static string getMimeFromFile(string file)
    {
        IntPtr mimeout;
        if (!System.IO.File.Exists(file))
        throw new FileNotFoundException(file + " not found");

        int MaxContent = (int)new FileInfo(file).Length;
        if (MaxContent > 4096) MaxContent = 4096;
        FileStream fs = File.OpenRead(file);


        byte[] buf = new byte[MaxContent];        
        fs.Read(buf, 0, MaxContent);
        fs.Close();
        int result = FindMimeFromData(IntPtr.Zero, file, buf, MaxContent, null, 0, out mimeout, 0);

        if (result != 0)
        throw Marshal.GetExceptionForHR(result);
        string mime = Marshal.PtrToStringUni(mimeout);
        Marshal.FreeCoTaskMem(mimeout);
        return mime;
    }
    //rename crystal.jpg to .gif to test functionality!
    string getImg = Environment.GetEnvironmentVariable("windir") + "\\Web\\WallPaper\\Crystal.gif";
        string mime = getMimeFromFile(getImg);
```

## VB.NET Sample Code:
```cs
Public Shared Function getMimeFromFile(ByVal file As String) As String
    Dim mimeout As IntPtr
    If Not System.IO.File.Exists(file) Then
        Throw New FileNotFoundException(file + " not found")
    End If
    Dim MaxContent As Integer = CInt(New FileInfo(file).Length)
    If MaxContent > 4096 Then
        MaxContent = 4096
    End If

    Dim fs As New FileStream(file, FileMode.Open)

    Dim buf(MaxContent) As Byte
    fs.Read(buf, 0, MaxContent)
    fs.Close()
    Dim result As Integer = FindMimeFromData(IntPtr.Zero, file, buf, MaxContent, Nothing, 0, mimeout, 0)

    If result <> 0 Then
        'Throw Marshal.GetHRForExceptionresult)
    End If

    Dim mime As String = Marshal.PtrToStringUni(mimeout)
    Marshal.FreeCoTaskMem(mimeout)
    Return mime
    End Function 'getMimeFromFile

    ''' <summary>
    ''' The second to last parameter errors out if its data type is set to string.
    ''' </summary>
    ''' <param name="pBC"></param>
    ''' <param name="pwzUrl"></param>
    ''' <param name="pBuffer"></param>
    ''' <param name="cbSize"></param>
    ''' <param name="pwzMimeProposed"></param>
    ''' <param name="dwMimeFlags"></param>
    ''' <param name="mimeOut"></param>
    ''' <param name="dwReserved"></param>
    ''' <returns></returns>
    <DllImport("urlmon.dll", CharSet:=CharSet.Auto)>
    Private Function FindMimeFromData(
    ByVal pBC As IntPtr,
    <MarshalAs(UnmanagedType.LPWStr)> ByVal pwzUrl As String,
    <MarshalAs(UnmanagedType.LPArray, ArraySubType:=UnmanagedType.I1, SizeParamIndex:=3)> ByVal pBuffer As Byte(),
    ByVal cbSize As Integer,
    <MarshalAs(UnmanagedType.LPWStr)> ByVal pwzMimeProposed As String,
    ByVal dwMimeFlags As Integer,
    ByRef mimeOut As IntPtr,
    ByVal dwReserved As Integer) As Integer
    End Function

    ''' <summary>
    ''' Written for use as an extension method for the byte array class.
    ''' </summary>
    ''' <param name="bytes"></param>
    ''' <param name="mimeContentType"></param>
    ''' <returns></returns>
    <Extension()>
    Public Function TryDetermineMimeType(
    bytes As Byte(),
    <Out()> ByRef mimeContentType As String) As Boolean

    Dim mimeSampleSize As Integer = 256
    Dim defaultMimeType As String = "application/octet-stream"
    Dim mimeOut As IntPtr = IntPtr.Zero
    Dim successful As Boolean = False
    mimeContentType = defaultMimeType
    Try
        FindMimeFromData(
        IntPtr.Zero,
        Nothing,
        bytes,
        Convert.ToUInt32(mimeSampleSize),
        Nothing,
        0,
        mimeOut,
        0)
        mimeContentType = Marshal.PtrToStringUni(mimeOut)
        Marshal.FreeCoTaskMem(mimeOut)
        successful = True
    Catch x As Exception
        Console.WriteLine(x.ToString())
    End Try
    Return successful
    End Function
```

## VB6 Sample Code:
```cs
Dim result As Long
  Dim bufferOut As String

  bufferOut = Space$(256)
  Dim buffAddr As Long
  buffAddr = StrPtr(bufferOut)

  result = FindMimeFromData(0, "file://c:/test/form1.frm", vbNullString, 0, vbNullString, 0, buffAddr, 0)
  Debug.Print PtrToString(buffAddr)
Click to read this page10/23/2022 7:47:26 PM - gBqsPxAZ-51.137.182.20Copies a block of memory from one location to another.4/22/2014 3:37:44 PM - -180.214.232.93ByVal is a VB keyword that specifies a variable to be passed as a parameter BY VALUE. In other words, if the function or sub changes the value of the internal variable, it does not change the value of the external variable that was passed to it.4/25/2007 3:19:55 AM - josep1er@cmich.edu-141.209.229.179ByVal is a VB keyword that specifies a variable to be passed as a parameter BY VALUE. In other words, if the function or sub changes the value of the internal variable, it does not change the value of the external variable that was passed to it.4/25/2007 3:19:55 AM - josep1er@cmich.edu-141.209.229.179An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29
```
