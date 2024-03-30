
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
  private struct Bluetooth_Find_Radio_Params
  {
    internal UInt32 dwSize;
     internal void Initialize()
     {
             this.dwSize = (UInt32)Marshal.SizeOf(typeof(Bluetooth_Find_Radio_Params));
     }
  }
```

## VB Definition:
```cs
Structure BLUETOOTH_FIND_RADIO_PARAMS 
   Public TODO
End Structure
```
