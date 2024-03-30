
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError=true)]
static extern IntPtr FindWindowA(string lpClassName, string lpWindowName);
```

## VB Signature:
```cs
Declare Function FindWindowA Lib "user32.dll" (lpClassName As String, lpWindowName As String) As Long
```

## Sample Code:
```cs
[DllImport("user32.dll", SetLastError = true)]
    static extern IntPtr FindWindowA(string lpClassName, string lpWindowName);

    private void test()
    {
    var handle = FindWindowA(null, "Untitled - Notepad");
    MessageBox.Show(handle.ToString() ?? "error");
    }
```
