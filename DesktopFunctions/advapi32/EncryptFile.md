
## C# Signature:
```cs
[DllImport("advapi32.dll", CharSet = CharSet.Auto, SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool EncryptFile(string filename);
```

## VB Signature:
```cs
Declare Function EncryptFile Lib "advapi32.dll" (TODO) As TODO
```

## C# Sample Code:
```cs
[DllImport("advapi32.dll", CharSet = CharSet.Auto, SetLastError=true)]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool EncryptFile(string filename);

string FileName = "C:\PATH\TO\YOUR\FILE";
if(EncryptFile(FileName)){
   //File encrypted
} else{
   throw new Exception("Encryption failed.");
}
```
