
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true)]
  static extern UInt32 WaitForSingleObject(IntPtr hHandle, UInt32 dwMilliseconds);
```

## VB.NET Signature:
```cs
<DllImport("kernel32", SetLastError := True)> _
  Function WaitForSingleObject( _
    ByVal handle As IntPtr, _
    ByVal milliseconds As UInt32) As UInt32
  End Function
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def WaitForSingleObject(hHandle as int, dwMilliseconds as long):
     pass
```

## Tips & Tricks:
```cs
const UInt32 INFINITE = 0xFFFFFFFF;
  const UInt32 WAIT_ABANDONED = 0x00000080;
  const UInt32 WAIT_OBJECT_0 = 0x00000000;
  const UInt32 WAIT_TIMEOUT = 0x00000102;

  and use:

  WaitForSingleObject(handle, (int)INFINITE);
```

## Tips & Tricks:
```cs
Const INFINITE As UInt32 = &HFFFFFFFFUI
  Const WAIT_ABANDONED As UInt32 = &H80UI
  Const WAIT_OBJECT_0 As UInt32 = &H0UI
  Const WAIT_TIMEOUT As UInt32 = &H102UI

  and use:

  WaitForSingleObject(handle, INFINITE)
```

## Sample Code:
```cs
private void Run()
{
  while (bRunning)
  {
   try 
    {
     if(WaitForSingleObject(ReceivedEvent,INFINITE) == WAIT_OBJECT_0)
     {
      // Signaled            
      DoSomething();
     }
    } 

    catch(Exception Ex)
    {
     // An exception occurred
     //
     trhow(Ex);
    } 
   }
}
```

## Sample Code:
```cs
UInt32 waitFor;
waitFor = WaitForSingleObject(hMutex, 10000);
if (waitFor == WAIT_TIMEOUT)
     throw new ....
else if (waitFor == WAIT_ABANDONED)
{
     ReleaseMutex(waitFor);
     throw new ....
}
if (waitFor != WAIT_OBJECT_0)
{
     throw new Win32Exception("Synchronization Mutex Error.");
}
return 0;
```
