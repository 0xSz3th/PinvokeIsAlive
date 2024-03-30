
## C# Signature:
```cs
[DllImport("shell32.dll")]
static extern int SHEmptyRecycleBin(IntPtr hWnd, string pszRootPath,
   uint dwFlags);
```

## Sample Code:
```cs
public class ShellBin
    {
        [DllImport("shell32.dll")]
        static extern int SHEmptyRecycleBin(IntPtr hWnd, string pszRootPath, uint dwFlags);

        //     No dialog box confirming the deletion of the objects will be displayed.
        const int SHERB_NOCONFIRMATION = 0x00000001;
        //     No dialog box indicating the progress will be displayed. 
        const int SHERB_NOPROGRESSUI = 0x00000002;
        //     No sound will be played when the operation is complete. 
        const int SHERB_NOSOUND = 0x00000004;

        public static void EmptyRecycleBin()
        {
            BinUtils.EmptyRecycleBin ( string.Empty );
        }

        public static void EmptyRecycleBin( string rootPath )
        {
            int hresult = SHEmptyRecycleBin(IntPtr.Zero, rootPath, 
                    SHERB_NOCONFIRMATION | SHERB_NOPROGRESSUI | SHERB_NOSOUND);
            System.Diagnostics.Debug.Write(hresult);
        }
    }
```
