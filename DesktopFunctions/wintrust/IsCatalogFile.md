
## C# Signature:
```cs
[DllImport("wintrust.dll")]
static extern bool IsCatalogFile(
     SafeFileHandle hFile,
     [MarshalAs(UnmanagedType.LPWStr)]
     String pwszFileName
);
```

## VB Signature:
```cs
Declare Function IsCatalogFile Lib "wintrust.dll" (TODO) As TODO
```

## Sample Code:
```cs
using Microsoft.Win32.SafeHandles;

// Sample to check if a file is a catalog by file name 
SafeFileHandle invalidHandle = new SafeFileHandle(new IntPtr(-1), true);
if (IsCatalogFile(invalidHandle, "c:\\my_catalog.cat"))
{
     MessageBox.Show("This file is a catalog");
}
else
{
     MessageBox.Show("This file is NOT a catalog");
}

// Sample to check if a file is a catalog by file handle
using (FileStream fs = new FileStream("c:\\my_catalog.cat", FileMode.Open))
{
     if (IsCatalogFile(fs.SafeFileHandle, null))
     {
         MessageBox.Show("This file is a catalog");
     }
     else
     {
         MessageBox.Show("This file is not a catalog");
     }
}
```
