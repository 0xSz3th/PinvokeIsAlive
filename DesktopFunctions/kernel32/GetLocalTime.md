
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern void GetLocalTime(out SYSTEMTIME lpSystemTime);
```

## VB Signature:
```cs
<DllImport("kernel32.dll")> _
Shared Sub GetLocalTime(ByRef time As SYSTEMTIME)
End Sub
```

## Sample Code in VB:
```cs
Imports System.Runtime.InteropServices

Public Class Class1
   <StructLayout(LayoutKind.Sequential)> _
   Private Structure SYSTEMTIME
     <MarshalAs(UnmanagedType.U2)> Public Year As Short
     <MarshalAs(UnmanagedType.U2)> Public Month As Short
     <MarshalAs(UnmanagedType.U2)> Public DayOfWeek As Short
     <MarshalAs(UnmanagedType.U2)> Public Day As Short
     <MarshalAs(UnmanagedType.U2)> Public Hour As Short
     <MarshalAs(UnmanagedType.U2)> Public Minute As Short
     <MarshalAs(UnmanagedType.U2)> Public Second As Short
     <MarshalAs(UnmanagedType.U2)> Public Milliseconds As Short
   End Structure

   <DllImport("kernel32.dll")> _
   Private Shared Sub GetLocalTime(ByRef time As SYSTEMTIME)
   End Sub

   Public Sub test1()
     Dim currenttime As SYSTEMTIME
     GetLocalTime(currenttime)

     Console.WriteLine("day: {0}", currenttime.Day)
     Console.WriteLine("dayofweek: {0}", currenttime.DayOfWeek)
     Console.WriteLine("month: {0}", currenttime.Month)
     Console.WriteLine("year: {0}", currenttime.Year)
     Console.WriteLine("hour: {0}", currenttime.Hour)
     Console.WriteLine("minute: {0}", currenttime.Minute)
     Console.WriteLine("second: {0}", currenttime.Second)
     Console.WriteLine("milliseconds: {0}", currenttime.Milliseconds)
   End Sub
End Class
```
