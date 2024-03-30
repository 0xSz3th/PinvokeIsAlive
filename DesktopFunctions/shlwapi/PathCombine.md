
## C# Signature:
```cs
[DllImport("shlwapi.dll", CharSet=CharSet.Auto)]
static extern string PathCombine([Out] StringBuilder lpszDest, string lpszDir, string lpszFile);
```

## VB.NET Signature
```cs
Declare Unicode Function PathCombine Lib "shlwapi.dll" Alias "PathCombineW" (<MarshalAs(UnmanagedType.LPTStr)> PathOut As System.Text.StringBuilder, <MarshalAs(UnmanagedType.LPTStr)> PathIn As String, <MarshalAs(UnmanagedType.LPTStr)> More As String) As IntPtr
```

## VB Signature:
```cs
Declare Function PathCombine Lib "shlwapi.dll" Alias "PathCombineA" (ByVal szDest As String, ByVal lpszDir As String, ByVal lpszFile As String) As Long
```

## Sample Code:
```cs
[DllImport("shlwapi.dll", CharSet = CharSet.Auto)]
    static extern string PathCombine([Out] StringBuilder lpszDest, string lpszDir, string lpszFile);
    public static string GetAbsolutePath(string basePath, string relativePath)
    {
        StringBuilder sb = new StringBuilder();
        return PathCombine(sb,basePath,relativePath);
    }

    //nunit test case
    [Test]
    public void TestGetAbsolutePath()
    {
        Assert.AreEqual(@"c:\abc\123.txt",IO.GetAbsolutePath(@"c:\abc\","123.txt"),"Test 1");
        Assert.AreEqual(@"c:\abc\123.txt", IO.GetAbsolutePath(@"c:\abc\efg\", @"..\123.txt"), "Test 1");

    }
```
