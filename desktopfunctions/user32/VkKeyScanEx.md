
## C# Signature:
```cs
[DllImport("user32.dll", CharSet = CharSet.Unicode)]
static extern short VkKeyScanEx(char ch, IntPtr dwhkl);
```

## VB.Net Signature:
```cs
<DllImport("user32.dll", CharSet := CharSet.Unicode)> _
Private Shared Function VkKeyScanEx(ch As Char, dwhkl As IntPtr) As Short
End Function
```

## Sample Code:
```cs
namespace KeyFinder
    {
      class Program
      {
    [DllImport("user32.dll", CharSet = CharSet.Unicode)]
    static extern short VkKeyScanEx(char ch, IntPtr dwhkl);
    [DllImport("user32.dll")]
    static extern bool UnloadKeyboardLayout(IntPtr hkl);
    [DllImport("user32.dll")]
    static extern IntPtr LoadKeyboardLayout(string pwszKLID, uint Flags);
    public class KeyboardPointer : IDisposable
    {
      private readonly IntPtr pointer;
      public KeyboardPointer(int klid)
      {
        pointer = LoadKeyboardLayout(klid.ToString("X8"), 1);
      }
      public KeyboardPointer(CultureInfo culture)
        :this(culture.KeyboardLayoutId){}
      public void Dispose()
      {
        UnloadKeyboardLayout(pointer);
        GC.SuppressFinalize(this);
      }
      ~KeyboardPointer()
      {
        UnloadKeyboardLayout(pointer);
      }
      // Converting to System.Windows.Forms.Key here, but
      // some other enumerations for similar tasks have the same
      // one-to-one mapping to the underlying Windows API values
      public bool GetKey(char character, out Keys key)
      {
        short keyNumber = VkKeyScanEx(character, pointer);
        if(keyNumber == -1)
        {
          key = System.Windows.Forms.Keys.None;
          return false;
        }
        key = (System.Windows.Forms.Keys)(((keyNumber & 0xFF00) << 8) | (keyNumber & 0xFF));
        return true;
      }
    }
    private static string DescribeKey(Keys key)
    {
      StringBuilder desc = new StringBuilder();
      if((key & Keys.Shift) != Keys.None)
        desc.Append("Shift: ");
      if((key & Keys.Control) != Keys.None)
        desc.Append("Control: ");
      if((key & Keys.Alt) != Keys.None)
        desc.Append("Alt: ");
      return desc.Append(key & Keys.KeyCode).ToString();
    }
    public static void Main(string[] args)
    {
      string testChars = "Aéש";
      Keys key;
      foreach(var culture in (new string[]{"he-IL", "en-US", "en-IE"}).Select(code => CultureInfo.GetCultureInfo(code)))
      {
        Console.WriteLine(culture.Name);
        using(var keyboard = new KeyboardPointer(culture))
          foreach(char test in testChars)
          {
        Console.Write(test);
        Console.Write('\t');
        if(keyboard.GetKey(test, out key))
          Console.WriteLine(DescribeKey(key));
        else
          Console.WriteLine("No Key");
          }
      }
      Console.Read();//Stop window closing
    }
      }
    }
```

## Sample Code:
```cs
he-IL
    A  Shift: A
    é  No Key
    ש  A
    en-US
    A  Shift: A
    é  No Key
    ש  No Key
    en-IE
    A  Shift: A
    é  Control: Alt: E
    ש  No Key
```
