
## C# Signature:
```cs
// NATIVE SUPPORT
IntPtr handle;
```

## VB Signature:
```cs
Declare Function IntPtr Lib "user32.dll" (TODO) As TODO
```

## Sample Code:
```cs
// A Windows Service example.

       IntPtr handle = this.ServiceHandle;

        myServiceStatus.currentState = (int)State.SERVICE_START_PENDING;   //0x00000002
        myServiceStatus.checkPoint = 1;
        myServiceStatus.waitHint = 5000;
        SetServiceStatus(handle, ref myServiceStatus);
```
