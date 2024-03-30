
## C# Signature:
```cs
[DllImport("shell32.dll", CharSet = CharSet.Ansi)]
public static extern void SHAddToRecentDocs(ShellAddToRecentDocsFlags flag, string path);

[DllImport("shell32.dll")]
public static extern void SHAddToRecentDocs(ShellAddToRecentDocsFlags flag, IntPtr pidl);
```

## User-Defined Types:
```cs
public enum ShellAddToRecentDocsFlags {
   Pidl = 0x001,
   Path = 0x002,
}
```

## Tips & Tricks:
```cs
public static void AddToRecentDocs(string path) {
   SHAddToRecentDocs(ShellAddToRecentDocsFlags.Path, path);
}
```

## Sample Code:
```cs
public enum ShellAddToRecentDocsFlags {
    Pidl = 0x001,
    Path = 0x002,
  }

  [DllImport("shell32.dll", CharSet = CharSet.Ansi)]
  public static extern void
    SHAddToRecentDocs(ShellAddToRecentDocsFlags flag, string path);

  [DllImport("shell32.dll")]
  public static extern void
    SHAddToRecentDocs(ShellAddToRecentDocsFlags flag, IntPtr pidl);

  public static void AddToRecentDocs(string path) {
    SHAddToRecentDocs(ShellAddToRecentDocsFlags.Path, path);
  }
```

## Sample Code:
```cs
...
  void OpenDocument(string newFilename) {
    ...
    // Put the file into the Start->Documents list
    ShellApi.AddToRecentDocs(newFilename);
  }

  void SaveDocument(string newFilename) {
    ...
    // Put the file into the Start->Documents list
    ShellApi.AddToRecentDocs(newFilename);
  }
  ...
```
