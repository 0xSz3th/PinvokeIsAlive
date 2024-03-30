
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern bool SetSystemTime(ref SYSTEMTIME time);
```

## VB Signature:
```cs
<DllImport("kernel32.dll")> _
Shared Function SetSystemTime(ByRef time As SYSTEMTIME) As Boolean
End Function
```

## Sample Code:
```cs
using System;
using System.Runtime.InteropServices;

namespace SystemDateTime
{
    class Class1
    {    /// <summary> This structure represents a date and time. </summary>
        public struct SYSTEMTIME 
        {    public ushort wYear,wMonth,wDayOfWeek,wDay,
                wHour,wMinute,wSecond,wMilliseconds;
        }

        /// <summary>
        /// This function retrieves the current system date
        /// and time expressed in Coordinated Universal Time (UTC).
        /// </summary>
        /// <param name="lpSystemTime">[out] Pointer to a SYSTEMTIME structure to
        /// receive the current system date and time.</param>
        [DllImport("kernel32.dll")]
        public extern static void GetSystemTime(ref SYSTEMTIME lpSystemTime);

        /// <summary>
        /// This function sets the current system date
        /// and time expressed in Coordinated Universal Time (UTC).
        /// </summary>
        /// <param name="lpSystemTime">[in] Pointer to a SYSTEMTIME structure that
        /// contains the current system date and time.</param>
        [DllImport("kernel32.dll")]
        public extern static uint SetSystemTime(ref SYSTEMTIME lpSystemTime);

        static void Main()
        {    Console.WriteLine(DateTime.Now.ToString());
            SYSTEMTIME st = new SYSTEMTIME();
            GetSystemTime(ref st);
            Console.WriteLine("Adding 1 hour...");
            st.wHour = (ushort)(st.wHour + 1 % 24);
            if (SetSystemTime(ref st) == 0)
                Console.WriteLine("FAILURE: SetSystemTime failed");
            Console.WriteLine(DateTime.Now.ToString());
            Console.WriteLine("Setting time back...");
            st.wHour = (ushort)(st.wHour - 1 % 24);
            SetSystemTime(ref st);
            Console.WriteLine(DateTime.Now.ToString());
            Console.WriteLine("Press Enter to exit");
            Console.Read();
        }
    }
}
```
