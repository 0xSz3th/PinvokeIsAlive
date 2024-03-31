
## C# Signature:
```cs
[StructLayout( LayoutKind.Sequential )]
    struct LASTINPUTINFO
    {
        public static readonly int SizeOf = Marshal.SizeOf(typeof(LASTINPUTINFO));

        [MarshalAs(UnmanagedType.U4)]
        public UInt32 cbSize;    
        [MarshalAs(UnmanagedType.U4)]
        public UInt32 dwTime;
    }
```

## VB .NET Signature:
```cs
<StructLayout(LayoutKind.Sequential)> _
    Structure LASTINPUTINFO
    <MarshalAs(UnmanagedType.U4)> _
    Public cbSize As Integer
    <MarshalAs(UnmanagedType.U4)> _
    Public dwTime As Integer
    End Structure
```

## F# 4.1 Signature
```cs
[<Struct; CLIMutable; StructLayout(LayoutKind.Sequential)>]
   type LastInputInfo = {
     size : int
     dwTime : uint32
   }
```
