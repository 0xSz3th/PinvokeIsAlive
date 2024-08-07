
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool SetLocalTime([In] ref SYSTEMTIME lpLocalTime);
```

## VB Signature:
```cs
<DllImport("kernel32.dll")> _
Shared Function SetLocalTime(ByRef time As SYSTEMTIME) As Boolean
End Function
```

## Tips & Tricks:
```cs
//I have added some methods to structure SYSTEMTIME. After that the convertion between System.DateTime and SYSTEM became much easier. :)
    //Sample Code in C#:

    //Sample code for SetLocalTime and SYSTEMTIME structure
    //Author:    Yuan Xiaohui from www.farproc.com 
    //Time :    August 30th, 2005

    using System;
    using System.Runtime.InteropServices;

    public class MyClass1
    {
        /// <summary>
        /// SYSTEMTIME structure with some useful methods
        /// </summary>
        public struct SYSTEMTIME
        {
            public ushort wYear;
            public ushort wMonth;
            public ushort wDayOfWeek;
            public ushort wDay;
            public ushort wHour;
            public ushort wMinute;
            public ushort wSecond;
            public ushort wMilliseconds;

            /// <summary>
            /// Convert form System.DateTime
            /// </summary>
            /// <param name="time"></param>
            public void FromDateTime(DateTime time)
            {
                wYear = (ushort)time.Year;
                wMonth = (ushort)time.Month;
                wDayOfWeek = (ushort)time.DayOfWeek;
                wDay = (ushort)time.Day;
                wHour = (ushort)time.Hour;
                wMinute = (ushort)time.Minute;
                wSecond = (ushort)time.Second;
                wMilliseconds = (ushort)time.Millisecond;
            }

            /// <summary>
            /// Convert to System.DateTime
            /// </summary>
            /// <returns></returns>
            public DateTime ToDateTime()
            {
                return new DateTime(wYear, wMonth, wDay, wHour, wMinute, wSecond, wMilliseconds);
            }
            /// <summary>
            /// STATIC: Convert to System.DateTime
            /// </summary>
            /// <param name="time"></param>
            /// <returns></returns>
            public static DateTime ToDateTime(SYSTEMTIME time)
            {
                return time.ToDateTime();
            }
        }

        //SetLocalTime C# Signature
        [DllImport("Kernel32.dll")]
        public static extern bool SetLocalTime( ref SYSTEMTIME Time );
```

## Tips & Tricks:
```cs
//Example
        private void Add7Days

        {
            //Get current time and add 7 days to it
            DateTime t = DateTime.Now.AddDays(7);
            //Convert to SYSTEMTIME
            SYSTEMTIME st = new SYSTEMTIME();
            st.FromDateTime(t);
            //Call Win32 API to set time
            SetLocalTime(ref st);
        }
    }
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

   <DllImport("kernel32.dll")> _
   Private Shared Function SetLocalTime(ByRef time As SYSTEMTIME) As Boolean
   End Function

   Public Sub SetsLocalTimeHourToEight()
     Dim currentTime As SYSTEMTIME
     GetLocalTime(currentTime)

     currentTime.Hour = 8

     SetLocalTime(currentTime)
   End Sub
End Class
```
