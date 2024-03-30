
## C# Signature:
```cs
[DllImport("wininet.dll", SetLastError = true, CharSet=CharSet.Auto)]
public static extern bool InternetSetOption(IntPtr hInternet, int
dwOption, IntPtr lpBuffer, int dwBufferLength);
```

## VB Signature:
```cs
<DllImport("wininet.dll", SetLastError:=True, CharSet:=CharSet.Auto)> _
Public Shared Function InternetSetOption(hInternet As IntPtr, dwOption As Integer, lpBuffer As IntPtr, dwBufferLength As Integer) As Boolean
End Function
```

## Sample Code:
```cs
public struct Struct_INTERNET_PROXY_INFO 
{ 
     public int dwAccessType; 
     public IntPtr proxy; 
     public IntPtr proxyBypass; 
}; 

[DllImport("wininet.dll", SetLastError = true)] 
     private static extern bool InternetSetOption(IntPtr hInternet, 
     int dwOption, 
     IntPtr lpBuffer, 
     int lpdwBufferLength); 

private void RefreshIESettings(string strProxy) 
{ 
     const int INTERNET_OPTION_PROXY = 38; 
     const int INTERNET_OPEN_TYPE_PROXY = 3;  

     Struct_INTERNET_PROXY_INFO struct_IPI; 

     // Filling in structure 
     struct_IPI.dwAccessType = INTERNET_OPEN_TYPE_PROXY; 
     struct_IPI.proxy = Marshal.StringToHGlobalAnsi(strProxy); 
     struct_IPI.proxyBypass = Marshal.StringToHGlobalAnsi("local"); 

     // Allocating memory 
     IntPtr intptrStruct = Marshal.AllocCoTaskMem(Marshal.SizeOf(struct_IPI)); 

     // Converting structure to IntPtr 
     Marshal.StructureToPtr(struct_IPI, intptrStruct, true); 

     bool iReturn = InternetSetOption(IntPtr.Zero, INTERNET_OPTION_PROXY, intptrStruct, Marshal.SizeOf(struct_IPI)); 
}  

private void SomeFunc() 
{ 
     RefreshIESettings("1.2.3.4:8080"); 
     //or RefreshIESettings("http://1.2.3.4:8080"); //both worked 
     //or RefreshIESettings("http=1.2.3.4:8080"); //both worked 

     System.Object nullObject = 0; 
     string strTemp = ""; 
     System.Object nullObjStr = strTemp; 
     axWebBrowser1.Navigate("http://willstay.tripod.com", ref nullObject, ref nullObjStr, ref nullObjStr, ref nullObjStr); 
}
```
