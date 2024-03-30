
## C# Signature:
```cs
/// <summary>Deletes a logical pen, brush, font, bitmap, region, or palette, freeing all system resources associated with the object. After the object is deleted, the specified handle is no longer valid.</summary>
/// <param name="hObject">A handle to a logical pen, brush, font, bitmap, region, or palette.</param>
/// <returns>
///   <para>If the function succeeds, the return value is nonzero.</para>
///   <para>If the specified handle is not valid or is currently selected into a DC, the return value is zero.</para>
/// </returns>
/// <remarks>
///   <para>Do not delete a drawing object (pen or brush) while it is still selected into a DC.</para>
///   <para>When a pattern brush is deleted, the bitmap associated with the brush is not deleted. The bitmap must be deleted independently.</para>
/// </remarks>
[DllImport("gdi32.dll", EntryPoint = "DeleteObject")]
[return: MarshalAs(UnmanagedType.Bool)]
public static extern bool DeleteObject([In] IntPtr hObject);
```

## VB.Net Signature:
```cs
<DllImport("gdi32.dll")> _
Private Shared Function DeleteObject(hObject As IntPtr)  As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## VB Signature:
```cs
Public Declare Function DeleteObject Lib "gdi32.dll" _
          (ByVal hObject As Long) As Long
```

## Tips & Tricks:
```cs
[C#]
public static Bitmap FromHbitmap(
    IntPtr hbitmap
);
```
