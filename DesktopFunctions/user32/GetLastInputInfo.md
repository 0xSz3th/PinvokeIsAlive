
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern bool GetLastInputInfo(ref LASTINPUTINFO plii);
```

## VB Signature:
```cs
<DllImport("user32.dll")>
Shared Function GetLastInputInfo(ByRef plii As LASTINPUTINFO) As Boolean
End Function
```

## C++ Signature:
```cs
[DllImport("user32.dll")]
static bool GetLastInputInfo(LASTINPUTINFO* plii);
```

## F# Signature
```cs
[<Struct; CLIMutable; StructLayout(LayoutKind.Sequential)>]
   type LastInputInfo = {
     size : int
     dwTime : uint32
   }

   [<DllImport("user32")>]
   extern int GetLastInputInfo(LastInputInfo& lpi);
```

## Sample Code:
```cs
static uint GetLastInputTime()
    {
        uint idleTime = 0;
        LASTINPUTINFO lastInputInfo = new LASTINPUTINFO();
        lastInputInfo.cbSize = (uint)Marshal.SizeOf( lastInputInfo );
        lastInputInfo.dwTime = 0;

        uint envTicks = (uint)Environment.TickCount;

        if ( GetLastInputInfo( ref lastInputInfo ) )
        {
        uint lastInputTick = lastInputInfo.dwTime;

        idleTime = envTicks - lastInputTick;
        }

        return (( idleTime > 0 ) ? ( idleTime / 1000 ) : 0);
    }
```

## Sample Code vb.net: 
```cs
Dim idletime As Integer
Dim lastInputInf As New LASTINPUTINFO()

   Public Function GetLastInputTime() As Integer

    idletime = 0
    lastInputInf.cbSize = Marshal.SizeOf(lastInputInf)
    lastInputInf.dwTime = 0

    If GetLastInputInfo(lastInputInf) Then
        idletime = Environment.TickCount - lastInputInf.dwTime
    End If

    If idletime > 0 Then
        Return idletime / 1000
    Else : Return 0
    End If

   End Function
```

## Sample Code C++ .net: 
```cs
public: static double getSystemIdleTime()
{                    
    int systemUptime = Environment::TickCount;
    int idleTicks = 0;
    LASTINPUTINFO lastInputInfo;
    lastInputInfo.cbSize = (UInt32)Marshal::SizeOf(lastInputInfo);
    lastInputInfo.dwTime = 0;
    if (GetLastInputInfo(&lastInputInfo))
    {        
        int lastInputTicks = (int)lastInputInfo.dwTime;
        idleTicks = systemUptime - lastInputTicks;
    }
    return (( idleTicks > 0 ) ? ( idleTicks / 1000 ) : idleTicks );
}
```

## Sample code F#
```cs
let idleTimeSeconds() =
     let size = Marshal.SizeOf (typeof<LastInputInfo>)
     let now = uint32 Environment.TickCount
     let mutable info = { size = size; dwTime = 0u }
     match GetLastInputInfo(&info) with
     | 0 -> 0.
     | _ ->
     let idleTicks = now - info.dwTime
     (float idleTicks) / 1000.
```

## Sample code gcc Cygwin:
```cs
#include <w32api/windef.h>
#include <w32api/winbase.h>
#include <w32api/winuser.h>

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int systemUptime = GetTickCount();    // was Environment.TickCount
    int idleTicks = 0;

    LASTINPUTINFO lastInputInfo;
    lastInputInfo.cbSize = sizeof (lastInputInfo);
    lastInputInfo.dwTime = 0;
    if (GetLastInputInfo(&lastInputInfo)) {        
        int lastInputTicks = (int)lastInputInfo.dwTime;
        idleTicks = systemUptime - lastInputTicks;
    }
    printf("%d seconds\n", (idleTicks > 0)? idleTicks/1000: 0);
    return 0;
}
```
