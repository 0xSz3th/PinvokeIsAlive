
## C# Signature:
```cs
[DllImport("shlwapi.dll", CharSet=CharSet.Auto)]
static extern bool PathCompactPathEx([Out] StringBuilder pszOut, string szPath, int cchMax, int dwFlags);
```

## VB.NET Signature:
```cs
''' <summary>
''' Truncates a path to fit within a certain number of characters by replacing path components with ellipses.
''' </summary>
''' <param name="pszOut">The address of the string that has been altered.</param>
''' <param name="pszSrc">A pointer to a null-terminated string of length MAX_PATH that contains the path to be altered.</param>
''' <param name="cchMax">
''' The maximum number of characters to be contained in the new string, including the terminating null character. 
''' For example, if cchMax = 8, the resulting string can contain a maximum of 7 characters plus the terminating null character.
''' </param>
''' <param name="reserved">Reserved</param>
''' <returns>Returns TRUE if successful, or FALSE otherwise.</returns>
<DllImport("shlwapi.dll", EntryPoint:="PathCompactPathExW",  SetLastError:=True, CharSet:=CharSet.Unicode)> 
Shared Public Function PathCompactPathEx(
                      <MarshalAs(UnmanagedType.LPTStr)> pszOut As System.Text.StringBuilder,
                      <MarshalAs(UnmanagedType.LPTStr)> pszSrc As String,
                      cchMax As UInteger,
                      reserved As Integer
                      ) As <MarshalAs(UnmanagedType.Bool)> Boolean
    End Function
```

## VB Signature:
```cs
Public Declare Function PathCompactPathEx Lib "shlwapi" Alias "PathCompactPathExA" _
        (ByVal pszOut As String, _
         ByVal pszSrc As String, _
         ByVal cchMax As Long, _
         ByVal dwFlags As Long) As Long
```

## C# Example
```cs
using System;
using System.Runtime.InteropServices;
using System.Text;

namespace CompactPathCmd
{
    /// <summary>
    /// Test code for PathCompactPathEx
    /// </summary>
    class Program
    {
        /// <summary>
        /// The main entry point for the application.
        /// </summary>
        [STAThread]
        static void Main(string[] args)
        {
            string longPath = "c:\\a\\very\\very\\long\\path\\that\\needs\\to\\be\\shortened\\by\\calling\\the\\PathCompactpathEx";
            int length = 40;

            string result = CompactPath(longPath, length);
            Console.WriteLine("     1     2     3     4     5     6     7");
            Console.WriteLine("1234567890123456789012345678901234567890123456789012345678901234567890123456789");
            Console.WriteLine(result);
            // displays : "c:\a\very\very\long...\PathCompactpathEx"
        }

        [DllImport("shlwapi.dll", CharSet=CharSet.Auto)]
        static extern bool PathCompactPathEx([Out] StringBuilder pszOut, string szPath, int cchMax, int dwFlags);

        public static string CompactPath(string longPathName, int wantedLength)
        {
            // NOTE: You need to create the builder with the required capacity before calling function.
            // See http://msdn.microsoft.com/en-us/library/aa446536.aspx
            StringBuilder sb = new StringBuilder(wantedLength + 1);
            PathCompactPathEx(sb, longPathName, wantedLength + 1, 0);
            return sb.ToString();
        }

    }

}
```

## VB Example
```cs
Private Function CompactPath(path As String) As String

        Const MAX_WIDTH As Integer = 79

        If path.Length <= MAX_WIDTH Then Return path
```

## VB Example
```cs
' NOTE: You need to create the builder with the required capacity before calling function.
        ' See http://msdn.microsoft.com/en-us/library/aa446536.aspx
        Dim sb As New Text.StringBuilder(MAX_WIDTH + 1)
        PathCompactPathEx(sb, path, MAX_WIDTH + 1, 0)
        Return sb.ToString()

    End Function
```
