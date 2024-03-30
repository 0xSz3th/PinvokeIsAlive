
## C# Signature:
```cs
[DllImport("setupapi.dll", CharSet = CharSet.Auto, SetLastError = true)]
static extern bool SetupDiClassNameFromGuid(
    Guid ClassGuid,
    StringBuilder ClassName,
    UInt32 ClassNameSize,
    out UInt32 RequiredSize
    );
```

## Sample Code:
```cs
StringBuilder className = null;
  uint classNameLen;
  SetupDiClassNameFromGuid(setupClass, className, 0, out classNameLen);
  className = new StringBuilder((int)classNameLen);
  if (!SetupDiClassNameFromGuid(setupClass, className, classNameLen, out classNameLen))
  {
    // Handle the error.
  }
  else
  {
    // Use the class name, e.g. Console.WriteLine(className.ToString());
  }
```
