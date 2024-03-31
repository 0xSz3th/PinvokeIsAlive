
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, Pack=1)]
    public struct TBBUTTON 
    {
        public int iBitmap;
        public int idCommand;
        public byte fsState;
        public byte fsStyle;
        public byte bReserved0;
        public byte bReserved1;
        public int dwData;
        public int iString;
    }
```

## VB Definition:
```cs
Public Structure TBBUTTON
        Public iBitmap As Integer
        Public idCommand As Integer
        Public fsState As Byte
        Public fsStyle As Byte
        Public bReserved0 As Byte
        Public bReserved1 As Byte
        Public dwData As Integer
        Public iString As Integer
    End Structure
```
