
## C# Signature:
```cs
[DllImport("userenv.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool GetProfilesDirectory(StringBuilder path, ref int size);
```

## Sample Code:
```cs
StringBuilder path = new StringBuilder(4*1024);
   int size = path.Capacity;
   if (GetProfilesDirectory(path, ref size) )
   {
       ... use path value, size contains length...
   }
```

## Sample code using gcc in Cygwin as a GUI w/ ICON executable
```cs
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

#include <windows.h>
#include <w32api/windows.h>
#include <w32api/userenv.h>

int main() {
    DWORD size = 4*1024;
    char *path = malloc(size);
    if (GetProfilesDirectory(path, &size) ) {
        printf("%d %s\n", (int)size, path);
        MessageBox(NULL, path, "GetProfilesDirectory()", MB_OK);
    }
    return 0;
}
```

## Sample code using gcc in Cygwin as a GUI w/ ICON executable
```cs
echo 'this ICON bfe.ico' > this.rc

windres this.rc -O coff -o this.res

gcc -Wall -Wl,--enable-stdcall-fixup -mnop-fun-dllimport -mwindows this.res usrprof.c /cygdrive/c/windows/system32/userenv.dll

./a.exe
```

## Sample code using gcc in Cygwin as a GUI w/ ICON executable
```cs
gcc -Wall -Wl,--enable-stdcall-fixup -mnop-fun-dllimport -mwindows usrprof.c /cygdrive/c/windows/system32/userenv.dll

./a.exe
```

## Sample code using mingw in Cygwin
```cs
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

#include <windows.h>

//#include "c:/cygwin/usr/include/w32api/userenv.h" USE THE FOLLOWING FROM HERE
WINBOOL WINAPI GetProfilesDirectoryA(LPSTR lpProfileDir, LPDWORD lpcchSize);

int main() {
    DWORD size = 4*1024;
    char *path = malloc(size);
    if (GetProfilesDirectory(path, &size) ) {
        printf("%d %s\n", (int)size, path);
        MessageBox(NULL, path, "GetProfilesDirectory()", MB_OK);
    }
    return 0;
}
```

## Sample code using mingw in Cygwin
```cs
i686-pc-mingw32-gcc -Wl,--enable-stdcall-fixup -Wall userprof.c /cygdrive/c/windows/system32/userenv.dll
```

## Sample code using mingw in Cygwin
```cs
./a.exe
```
