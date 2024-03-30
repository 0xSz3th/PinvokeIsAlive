
## Sample Code:
```cs
[DllImport("gdi32.dll")]
     static extern bool GetCharABCWidths(IntPtr hdc, uint uFirstChar,
    uint uLastChar, ref  ABC lpabc);

     [StructLayout(LayoutKind.Sequential)]
     public struct ABC
     { /* abc */
       public int abcA;
       public uint abcB;
       public int abcC;
      }

      /* Declare an array of 3 struct ABC */
      ABC[] abc = { new ABC(), new ABC(), new ABC() };

      /* put the adress of the first cell of the struct abc array */
      bool ret = GetCharABCWidths(Hdc, 'A', 'C', ref abc[0]);
```
