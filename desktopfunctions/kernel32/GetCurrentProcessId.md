
## C# Signature:
```cs
[DllImport("kernel32.dll")]
static extern uint GetCurrentProcessId();
```

## VB Signature:
```cs
Declare Function GetCurrentProcessId Lib "kernel32" () As Integer
```

## Boo Signature:
```cs
[DllImport("kernel32.dll")]
def GetCurrentProcessId() as int:
     pass
```

## Sample Code:
```cs
class FindMyself
  {
    [DllImport("kernel32.dll")]
    public static extern uint GetCurrentProcessId();
  }

  class WhoAmI
  {
    private void LookUp()
    {
      uint MyID = FindMyself.GetCurrentProcessId();
    }
  }
```

## Alternative Managed API:
```cs
Process.GetCurrentProcess().Id
```
