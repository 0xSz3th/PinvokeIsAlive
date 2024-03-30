
## C# Signature:
```cs
/// <summary>Deletes the specified device context (DC).</summary>
/// <param name="hdc">A handle to the device context.</param>
/// <returns><para>If the function succeeds, the return value is nonzero.</para><para>If the function fails, the return value is zero.</para></returns>
/// <remarks>An application must not delete a DC whose handle was obtained by calling the <c>GetDC</c> function. Instead, it must call the <c>ReleaseDC</c> function to free the DC.</remarks>
[DllImport("gdi32.dll", EntryPoint = "DeleteDC")]
public static extern bool DeleteDC([In] IntPtr hdc);
```

## VB.NET Signature:
```cs
<DllImport("gdi32.dll")> _
Private Shared Function DeleteDC(hdc As IntPtr) As <MarshalAs(UnmanagedType.Bool)> Boolean
End Function
```

## VB Signature:
```cs
Public Declare Function DeleteDC Lib "gdi32" _
          (ByVal hDC As Long) As Long
```
