
## C# Signature:
```cs
[DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
static extern IntPtr LoadImage(IntPtr hinst, string lpszName, uint uType,
   int cxDesired, int cyDesired, uint fuLoad);
```

## VB Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)> _
Private Shared Function LoadImage(ByVal hInst As IntPtr, ByVal lpszName As String, ByVal uType As UInt32, _
ByVal cxDesired As Integer, ByVal cyDesired As Integer, ByVal fuLoad As UInt32) As IntPtr
End Function
```

## C++/CLI Signature:
```cs
[DllImportAttribute("user32.dll", SetLastError = true, CharSet = CharSet::Auto)]
extern "C" int LoadImage(int hinst, int lpszName, unsigned int uType, int cxDesired, int cyDesired, unsigned int fuLoad);
```

## Sample Code:
```cs
using namespace System::Runtime::InteropServices;
using namespace System::Windows::Forms;
using namespace System::Reflection;

int a = LoadImage(Marshal::GetHINSTANCE(Assembly::GetExecutingAssembly()->GetModules()[0]).ToInt32(),101,2,0,0,0);
this->Cursor = gcnew ::Cursor(IntPtr(a));
```

## Sample Code (C#):
```cs
namespace ITLN.Utils.GUI {

    // http://www.itln.pl
    public static class AuxiliaryGUIIcon {

        [DllImport("user32.dll", SetLastError = true, CharSet = CharSet.Auto)]
        private static extern IntPtr LoadImage(IntPtr hinst, string lpszName, uint uType,
            int cxDesired, int cyDesired, uint fuLoad);

        [DllImport("user32.dll", SetLastError = true)]
        private static extern int DestroyIcon(IntPtr hIcon);

        [DllImport("kernel32.dll", SetLastError = true, CharSet = CharSet.Auto)]
        private static extern IntPtr LoadLibraryEx(string lpFileName, IntPtr hFile, LoadLibraryFlags dwFlags);

        private enum LoadLibraryFlags : uint {
            DONT_RESOLVE_DLL_REFERENCES = 0x00000001,
            LOAD_IGNORE_CODE_AUTHZ_LEVEL = 0x00000010,
            LOAD_LIBRARY_AS_DATAFILE = 0x00000002,
            LOAD_LIBRARY_AS_DATAFILE_EXCLUSIVE = 0x00000040,
            LOAD_LIBRARY_AS_IMAGE_RESOURCE = 0x00000020,
            LOAD_WITH_ALTERED_SEARCH_PATH = 0x00000008
        }

        /// <summary>
        /// Returns an icon of given size.
        /// </summary>
        /// <param name="path">Path to a file (.exe/.dll) that contains the icons.
        ///        Skip it or use <c>null</c> to use current application's file.</param>
        /// <param name="resId">Name of the resource icon that should be loaded.
        ///        Skip it to use the default <c>#32512</c> (value of <c>IDI_APPLICATION</c>) to use
        ///        the application's icon.</param>
        /// <param name="size">Size of the icon to load. If there is no such size available, a larger or smaller
        ///        sized-icon is scaled.</param>
        /// <returns>List of all icons.</returns>
        public static Icon GetIconFromExe(string path = null, string resId = "#32512", int size = 32) {
            // load module
            IntPtr h;
            if (path == null)
                h = Marshal.GetHINSTANCE(Assembly.GetEntryAssembly().GetModules()[0]);
            else {
                h = LoadLibraryEx(path, IntPtr.Zero, LoadLibraryFlags.LOAD_LIBRARY_AS_DATAFILE);
                if (h == IntPtr.Zero)
                    return null;
            }

            // 1 is IMAGE_ICON
            IntPtr ptr = LoadImage(h, resId, 1, size, size, 0);
            if (ptr != IntPtr.Zero) {
                try {
                    Icon icon = (Icon)Icon.FromHandle(ptr).Clone();
                    return icon;
                } finally {
                    DestroyIcon(ptr);
                }
            }
            return null;
        }
    }
}
```
