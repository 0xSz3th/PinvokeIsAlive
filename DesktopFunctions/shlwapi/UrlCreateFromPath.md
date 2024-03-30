
## C# Signature:
```cs
[DllImport("shlwapi.dll", CharSet=CharSet.Auto)]
    static extern int UrlCreateFromPath(
    [In]     string path,
    [Out]    StringBuilder url, 
    [In,Out] ref uint urlLength,
    [In]     uint reserved
    );
```

## VB Signature:
```cs
Declare Unicode Function UrlCreateFromPath Lib "shlwapi.dll" Alias "UrlCreateFromPathW" _
    (ByVal path As String, _
     ByVal url As System.Text.StringBuilder, _
     ByRef urlLength As System.UInt32, _
     ByVal reserved As Integer _
    ) As Integer
```

## Sample Code (C# console):
```cs
[STAThread]
    static void Main(string[] args)
    {
      Console.Write(@"Enter filename: ");
      string filename = Console.ReadLine();
      Console.WriteLine(UrlFromPath(filename));

      Console.Read();
    }

    private static string UrlFromPath(string filepath)
    {
      uint maxLen=2048+32+3;//see INTERNET_MAX_URL_LENGTH
      StringBuilder url = new StringBuilder((int)maxLen);
      UrlCreateFromPath(filepath,url,ref maxLen,0);
      return url.ToString();
    }
```

## Sample Code (VB winform):
```cs
Const INTERNET_MAX_URL_LENGTH As Integer = 2048 + 32 + 3

    Private Sub urlFromPathButton_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles urlFromPathButton.Click
      Dim sz As System.UInt32
      Dim sb As System.Text.StringBuilder
      Dim rc As Integer

      sz = Convert.ToUInt32(INTERNET_MAX_URL_LENGTH)
      sb = New System.Text.StringBuilder(INTERNET_MAX_URL_LENGTH)

      rc = UrlCreateFromPath(pathTextbox.Text, sb, sz, 0)

      urlTextbox.Text = sb.ToString()
    End Sub
```
