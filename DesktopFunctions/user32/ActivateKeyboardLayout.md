
## C# Signature:
```cs
public enum HKL{HKL_PREV, HKL_NEXT}
/// <summary>Sets the input locale identifier (formerly called the keyboard layout handle) for the calling thread or the current process. The input locale identifier specifies a locale as well as the physical layout of the keyboard</summary>
/// <param name="hkl">Input locale identifier to be activated.</param>
/// <param name="Flags">Specifies how the input locale identifier is to be activated.</param>
/// <returns>The return value is of type HKL. If the function succeeds, the return value is the previous input locale identifier. Otherwise, it is zero</returns>
[DllImport("user32.dll", SetLastError = true)]
internal static extern HKL ActivateKeyboardLayout(HKL hkl, uint Flags);
```

## VB.Net Signature:
```cs
''' <summary>Sets the input locale identifier (formerly called the keyboard layout handle) for the calling thread or the current process. The input locale identifier specifies a locale as well as the physical layout of the keyboard</summary>
''' <param name="hkl">Input locale identifier to be activated.</param>
''' <param name="Flags">Specifies how the input locale identifier is to be activated.</param>
''' <returns>The return value is of type HKL. If the function succeeds, the return value is the previous input locale identifier.
<DllImport("user32.dll")> _
Public Shared Function ActivateKeyboardLayout(ByVal nkl As IntPtr, ByVal Flags As uint) As Integer
End Function
```

## Notes:
```cs
seealso KLF enum
seealso HKL enum
```
