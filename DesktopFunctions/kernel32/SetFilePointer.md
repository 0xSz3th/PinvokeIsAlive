
## C# Signature:
```cs
public enum EMoveMethod : uint
    {
        Begin = 0,
        Current = 1,
        End = 2
    }

    [DllImport("Kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern unsafe uint SetFilePointer(
        [In] SafeFileHandle hFile, 
        [In] int lDistanceToMove,
        [Out] int* lpDistanceToMoveHigh,
        [In] EMoveMethod dwMoveMethod);

    [DllImport("Kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    static extern uint SetFilePointer(
        [In] SafeFileHandle hFile, 
        [In] int lDistanceToMove,
        [Out] out int lpDistanceToMoveHigh,
        [In] EMoveMethod dwMoveMethod);
```

## VB Signature:
```cs
Public Enum EMoveMethod As System.UInt32
        FILE_BEGIN = 0
        FILE_CURRENT = 1
        FILE_END = 2
    End Enum

    <DllImport("kernel32.dll", SetLastError:=True)> _
    Shared Function SetFilePointer( _
        ByVal hFile As IntPtr, _
        ByVal lDistanceToMove As Integer, _
        ByRef lpDistanceToMoveHigh As IntPtr, _
        ByVal dwMoveMethod As EMoveMethod) _
        As System.UInt32
    End Function

    Public Const INVALID_SET_FILE_POINTER As Integer = -1
```

## Sample Code:
```cs
[DllImport("Kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
    private static extern int SetFilePointer(IntPtr handle, int lDistanceToMove, out int lpDistanceToMoveHigh, uint dwMoveMethod);

    public long Seek(IntPtr handle, long offset, SeekOrigin origin)
    {
    uint moveMethod = 0;

    switch (origin)
    {
        case SeekOrigin.Begin:
        moveMethod = 0;
        break;

        case SeekOrigin.Current:
        moveMethod = 1;
        break;

        case SeekOrigin.End:
        moveMethod = 2;
        break;
    }

    int lo = (int)(offset & 0xffffffff);
    int hi = (int)(offset >> 32);

    lo = SetFilePointer(handle, lo, out hi, moveMethod);

    if (lo == -1)
    {
        if (GetLastError() != 0)
        {
        throw new Exception("INVALID_SET_FILE_POINTER");
        }
    }

    return (((long)hi << 32) | (uint)lo);
    }
```
