
## C# Signature:
```cs
enum SetupUOInfFlags : uint { NONE = 0x0000, SUOI_FORCEDELETE = 0x0001 };

      [DllImport("setupapi.dll", SetLastError = true)]
      static extern bool SetupUninstallOEMInf(
      string InfFileName,
      SetupUOInfFlags Flags,
      IntPtr Reserved
     );
```

## VB Signature:
```cs
Declare Function SetupUninstallOEMInf Lib "setupapi.dll" (TODO) As TODO
```

## Sample Code:
```cs
public bool UninstallInfByText(string text)
{
   StringBuilder winDir = new StringBuilder(256);
   if (0 == GetWindowsDirectory(winDir, winDir.Capacity)) return (false);
   string infDir = winDir.ToString() + "\\inf";
   string[] infFiles = Directory.GetFiles(infDir, "*.inf");
   bool retval = true;
   foreach (string infFile in infFiles)
   {
      string inf = File.ReadAllText(infFile);
      if (inf.Contains(textBox1.Text))
      {
       string infFileName = infFile.Remove(0, infFile.LastIndexOf('\\') + 1);
       retval = retval&& (SetupUninstallOEMInf(infFileName, SetupUOInfFlags.SUOI_FORCEDELETE, IntPtr.Zero));
      }
   }
   return (retval);
}
```
