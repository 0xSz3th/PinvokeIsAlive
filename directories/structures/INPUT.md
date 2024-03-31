
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential)]
public struct INPUT
{
  internal InputType type;
  internal InputUnion U;
  internal static int Size
  {
   get { return Marshal.SizeOf(typeof(INPUT)); }
  }
}

public enum InputType : uint
{
  INPUT_MOUSE,
  INPUT_KEYBOARD,
  INPUT_HARDWARE
}

[StructLayout(LayoutKind.Explicit)]
internal struct InputUnion
{
  [FieldOffset(0)]
  internal MOUSEINPUT mi;
  [FieldOffset(0)]
  internal KEYBDINPUT ki;
  [FieldOffset(0)]
  internal HARDWAREINPUT hi;
}
```

## VB Definition:
```cs
<StructLayout(LayoutKind.Explicit)> _
Structure InputUnion
  <FieldOffset(0)> Public mi As MOUSEINPUT
  <FieldOffset(0)> Public ki As KEYBDINPUT
  <FieldOffset(0)> Public hi As HARDWAREINPUT
End Structure        

Structure INPUT
  Public type As Integer
  Public u As InputUnion
End Structure
```
