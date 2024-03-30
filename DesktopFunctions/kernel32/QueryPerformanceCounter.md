
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
static extern bool QueryPerformanceCounter(out long lpPerformanceCount);
```

## VB.NET Signature:
```cs
<DllImport("kernel32.dll", SetLastError:=True)> _
Shared Function QueryPerformanceCounter(ByRef lpPerformanceCount As Long) As Boolean
End Function
```

## Manage C++ Signature:
```cs
[DllImport("Kernel32.dll", SetLastError=true)]
extern bool QueryPerformanceCounter(long *lpPerformanceCount);
```

## Tips & Tricks:
```cs
[DllImport("kernel32.dll"),SuppressUnmanagedCodeSecurity]
static extern bool QueryPerformanceCounter(out long lpPerformanceCount);
```

## VB.NET Sample Code:
```cs
Imports System.Runtime.InteropServices
Imports System.Security

Friend Enum TimeState
    Started
    Stopped

End Enum

Public Class HighResTimer

    <DllImport("kernel32.dll"), SuppressUnmanagedCodeSecurity()> _
    Private Shared Function QueryPerformanceCounter(ByRef lpPerformanceCount As Long) As Boolean
    End Function
```

## VB.NET Sample Code:
```cs
<DllImport("kernel32.dll"), SuppressUnmanagedCodeSecurity()> _
    Private Shared Function QueryPerformanceFrequency(ByRef lpPerformanceFreq As Long) As Boolean
    End Function

    Private Shared freq As Long
    Shared Sub New()
    If Not QueryPerformanceFrequency(freq) Then

        Throw New System.ComponentModel.Win32Exception
    End If
    End Sub

    Private startTime, endTime As Long
    Private _duration As Double
    Private state As TimeState = TimeState.Stopped
```

## VB.NET Sample Code:
```cs
Public Sub Start()
    If state = TimeState.Started Then
        Throw New ApplicationException("Cant' start, already started")
    End If
    state = TimeState.Started
    QueryPerformanceCounter(startTime)
    End Sub

    Public Function [Stop]() As Double
    QueryPerformanceCounter(endTime)
    If state = TimeState.Stopped Then
        Throw New ApplicationException("Cant' start, already started")
    End If
    state = TimeState.Stopped
    _duration = ((endTime - startTime) / freq)
    Return _duration
    End Function

    Public ReadOnly Property Duration() As Double
    Get
        If state = TimeState.Started Then
        Throw New ApplicationException("Must call Stop() first")
        End If
        Return _duration
    End Get
    End Property

End Class
```

## C# Sample Code:
```cs
using System;
    using System.Runtime.InteropServices;

    public class HighResTimer {
    [DllImport("kernel32.dll", SetLastError = false)]
    private static extern bool QueryPerformanceCounter(out long lpPerformanceCount);

    [DllImport("kernel32.dll", SetLastError = false)]
    private static extern bool QueryPerformanceFrequency(out long lpPerformanceFreq);

    private static long freq;

    static HighResTimer() {
        if (!QueryPerformanceFrequency(out freq)) {
            throw new System.ComponentModel.Win32Exception();
        }
    }

    private long startTime, endTime;
    private double duration;

    private bool timerStarted;

    public void Start() {
        if (timerStarted) {
            throw new ApplicationException("Cant' start, already started");
        }

        timerStarted = true;
        QueryPerformanceCounter(out startTime);
    }

    public void Stop() {
        QueryPerformanceCounter(out endTime);

        if (!timerStarted) {
            throw new ApplicationException("Cant' start, already started");
        }

        duration = (((endTime - startTime) / (double)freq));

        timerStarted = false;
    }

    public double Duration {
        get {
            if (timerStarted) {
                throw new ApplicationException("Must call Stop() first");
            }
            return duration;
        }
        }
    }

    static void Main(string[] args) {
         HighResTimer hrtimer = new HighResTimer();
         hrtimer.Start();
         //some code... For example:
         System.Threading.Thread.Sleep(1000);
         //End example
         hrtimer.Stop();
         double time = hrtimer.Duration * 1000;

         Console.WriteLine("Time in miliseconds " + time.ToString());
    }
```
