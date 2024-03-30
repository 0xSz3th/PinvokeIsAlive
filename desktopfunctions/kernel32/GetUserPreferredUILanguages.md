
## C# Signature:
```cs
[DllImport("Kernel32.dll", CharSet = CharSet.Auto, SetLastError = true)]
static extern bool GetUserPreferredUILanguages(
   uint dwFlags,
   out uint pulNumLanguages,
   char[] pwszLanguagesBuffer,
   ref uint pcchLanguagesBuffer);
```

## Sample Code:
```cs
static void DisplayUserPref()
{
    uint languagesCount, languagesBufferSize = 0;

    if (GetUserPreferredUILanguages(
        MUI_LANGUAGE_NAME,
        out languagesCount,
        null,
        ref languagesBufferSize))
    {
        char[] languagesBuffer = new char[languagesBufferSize];
        if (GetUserPreferredUILanguages(
            MUI_LANGUAGE_NAME,
            out languagesCount,
            languagesBuffer,
            ref languagesBufferSize))
        {
            string[] languages = new string(languagesBuffer, 0, (int) languagesBufferSize - 2).Split('\0');
            Console.WriteLine("GetUserPreferredUILanguages returns " + languages.Length + " languages:");
            foreach (string language in languages)
                Console.WriteLine("   " + language);
        }
        else
            Console.WriteLine("GetUserPreferredUILanguages(2) returns #" + Marshal.GetLastWin32Error());
    }
    else
        Console.WriteLine("GetUserPreferredUILanguages(1) returns #" + Marshal.GetLastWin32Error());
}

const uint MUI_LANGUAGE_ID = 0x4;    // Use traditional language ID convention
const uint MUI_LANGUAGE_NAME = 0x8;    // Use ISO language (culture) name convention
```
