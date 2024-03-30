
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int TileWindows(IntPtr hwndParent, int wHow, IntPtr lpRect, int cKids, IntPtr lpKids);
```

## C# Signature:
```cs
[DllImport("user32.dll")]
static extern int TileWindows(IntPtr hwndParent, int wHow, IntPtr lpRect, int cKids, [MarshalAs(UnmanagedType.LPArray)]IntPtr[] lpKids);
```

## Tips & Tricks:
```cs
Private Shared Function EnumWindows(
```

## Tips & Tricks:
```cs
End Function
```

## Tips & Tricks:
```cs
Private Shared Function TileWindows(ByVal hwndParent As System.IntPtr, ByVal wHow As UInteger, ByVal lpRect As RECT, ByVal cKids As UInteger, ByVal lpKids() As System.IntPtr) As UShort
    End Function
```

## Tips & Tricks:
```cs
Private Shared Function GetWindowText(hWnd As IntPtr, lpString As StringBuilder, nMaxCount As Integer) As Integer
    End Function
```

## Tips & Tricks:
```cs
Dim sb As New StringBuilder(1024)
        GetWindowText(hwnd, sb, sb.Capacity)
        Return sb.ToString
    End Function
```

## Tips & Tricks:
```cs
Private Sub TileClassMatch(className As String, inRect As RECT, _
             partialMatch As Boolean)

        Dim hwndLst As New List(Of IntPtr)
        'Define the 'ad-hoc' routine as needed, e.g.:
        Dim CB As New EnumWindowsProc(Function(hwnd As IntPtr, lParam As IntPtr)
                                          Dim cln As String = GetWindowsTitle(hwnd)
                                          If partialMatch Then
                                              If className.ToLower.Contains(cln.ToLower) Then
                                                  hwndLst.Add(hwnd)
                                              End If
                                          Else
                                              If className = cln Then hwndLst.Add(hwnd)
                                          End If

                                          Return True
                                      End Function)
        'Call it...
        EnumWindows(CB, IntPtr.Zero)

        If hwndLst.Count > 0 Then
            Dim successCount As UShort = _
            TileWindows(IntPtr.Zero, MDI_TILE.SKIPDISABLED, _
             inRect, CUInt(hwndLst.Count), hwndLst.ToArray)
            MessageBox.Show(String.Concat(successCount.ToString, " windows tiled in ", vbCrLf, _
             "rectangle ", inRect.Left.ToString, ", ", inRect.Top.ToString, ", ", inRect.Right.ToString, _
             ", ", inRect.Bottom.ToString), "Tiling...", MessageBoxButtons.OK, MessageBoxIcon.Information)
        End If
    End Sub
```
