
## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Unicode)]
static extern uint GetPrivateProfileString(
   string lpAppName, 
   string lpKeyName,
   string lpDefault, 
   StringBuilder lpReturnedString, 
   uint nSize,
   string lpFileName);
```

## C# Signature:
```cs
[DllImport("kernel32.dll", CharSet=CharSet.Unicode)]
static extern uint GetPrivateProfileString(
   string lpAppName, 
   string lpKeyName,
   string lpDefault, 
   [In, Out] char[] lpReturnedString, 
   uint nSize,
   string lpFileName);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
    Private Shared Function GetPrivateProfileString(ByVal lpAppName As String, _
                            ByVal lpKeyName As String, _
                            ByVal lpDefault As String, _
                            ByVal lpReturnedString As StringBuilder, _
                            ByVal nSize As Integer, _
                            ByVal lpFileName As String) As Integer
    End Function
```

## C++ Signature:
```cs
[DllImport("KERNEL32.DLL", CharSet=CharSet::Auto, EntryPoint="GetPrivateProfileString")]
static UInt32 GetPrivateProfileString(
   String^ lpAppName,
   String^ lpKeyName,
   String^ lpDefault,
   StringBuilder^ lpReturnedString,
   UInt32 nSize,
   String^ lpFileName);
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;
using System.Text;
namespace GPPS
{
   class Class1
   {
     static void Main(string[] args)
     {
       StringBuilder sb = new StringBuilder(500);
       uint res = GetPrivateProfileString("AppName", "KeyName", "", sb, (uint)sb.Capacity, @"c:\test.ini");
       Console.WriteLine(sb.ToString());
     }
       [DllImport("kernel32.dll")]
       static extern uint GetPrivateProfileString(
     string lpAppName, string lpKeyName, string lpDefault, StringBuilder lpReturnedString, int nSize, string lpFileName);
   }
}
```

## Sample Code:
```cs
Imports System.Runtime.InteropServices
Imports System.Text
Module1
    Private Declare Auto Function GetPrivateProfileString Lib "kernel32" (ByVal lpAppName As String, _
                ByVal lpKeyName As String, _
                ByVal lpDefault As String, _
                ByVal lpReturnedString As StringBuilder, _
                ByVal nSize As Integer, _
                ByVal lpFileName As String) As Integer

    Sub Main()

    Dim res As Integer
    Dim sb As StringBuilder

    sb = New StringBuilder(500)
    res = GetPrivateProfileString("AppName", "KeyName", "", sb, sb.Capacity, "c:\test.ini")
    Console.WriteLine("GetPrivateProfileStirng returned : " & res.ToString())
    Console.WriteLine("KeyName is : " & sb.ToString())

    End Sub
End Module
```
