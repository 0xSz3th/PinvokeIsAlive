
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet=CharSet.Unicode)]
private static extern int PickIconDlg(IntPtr hwndOwner, System.Text.StringBuilder lpstrFile, int nMaxFile, ref int lpdwIconIndex);
```

## VB Signature:
```cs
Declare Unicode Function PickIconDlg Lib "Shell32" Alias "PickIconDlg" (ByVal hwndOwner As IntPtr, ByVal lpstrFile As String, ByVal nMaxFile As Integer, ByRef lpdwIconIndex As Integer) As Integer
```

## Sample Code:
```cs
string iconfile;
int iconindex = 0;
int retval;
System.Text.StringBuilder sb;

iconfile = Environment.GetFolderPath(Environment.SpecialFolder.System);
iconfile = iconfile + @"\shell32.dll";
sb = new System.Text.StringBuilder(iconfile, 500);
retval = PickIconDlg(this.Handle, sb, sb.Length + 1, ref iconindex);
iconfile = sb.ToString();
```

## Sample Code:
```cs
retval = PickIconDlg(this.Handle, sb, sb.Capacity, ref iconindex);
```
