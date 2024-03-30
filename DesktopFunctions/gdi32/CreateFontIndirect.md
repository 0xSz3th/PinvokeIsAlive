
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr CreateFontIndirect([In] ref LOGFONT lplf);
```

## Tips & Tricks:
```cs
[DllImport("gdi32.dll", CharSet=CharSet.Auto)]
      public static extern IntPtr CreateFontIndirect(
        [In, MarshalAs(UnmanagedType.LPStruct)]
        LOGFONT lplf   // characteristics
        );
```
