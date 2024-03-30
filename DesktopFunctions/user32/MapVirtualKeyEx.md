
## C# Signature:
```cs
[DllImport("user32.dll")]
static extern uint MapVirtualKeyEx(uint uCode, uint uMapType, IntPtr dwhkl);
```

## C# Signature:
```cs
[DllImport("user32.dll")]
static extern uint MapVirtualKeyEx(uint uCode, MapVirtualKeyMapTypes uMapType, IntPtr dwhkl);
```

## VB.NET Signature:
```cs
Declare Unicode Function MapVirtualKeyEx Lib "user32.dll" Alias "MapVirtualKeyExW" (uCode As UInteger, uMapType As UInteger, dwhkl As IntPtr) As UInteger
```

## C# User-Defined Types:
```cs
const uint MAPVK_VK_TO_VSC = 0x00;
const uint MAPVK_VSC_TO_VK = 0x01;
const uint MAPVK_VK_TO_CHAR = 0x02;
const uint MAPVK_VSC_TO_VK_EX = 0x03;
const uint MAPVK_VK_TO_VSC_EX = 0x04;
```

## C# User-Defined Types:
```cs
/// <summary>
/// The set of valid MapTypes used in MapVirtualKey
/// </summary>
public enum MapVirtualKeyMapTypes : uint
{
     /// <summary>
     /// uCode is a virtual-key code and is translated into a scan code.
     /// If it is a virtual-key code that does not distinguish between left- and
     /// right-hand keys, the left-hand scan code is returned.
     /// If there is no translation, the function returns 0.
     /// </summary>
     MAPVK_VK_TO_VSC = 0x00,

     /// <summary>
     /// uCode is a scan code and is translated into a virtual-key code that
     /// does not distinguish between left- and right-hand keys. If there is no
     /// translation, the function returns 0.
     /// </summary>
     MAPVK_VSC_TO_VK = 0x01,

     /// <summary>
     /// uCode is a virtual-key code and is translated into an unshifted
     /// character value in the low-order word of the return value. Dead keys (diacritics)
     /// are indicated by setting the top bit of the return value. If there is no
     /// translation, the function returns 0.
     /// </summary>
     MAPVK_VK_TO_CHAR = 0x02,

     /// <summary>
     /// Windows NT/2000/XP: uCode is a scan code and is translated into a
     /// virtual-key code that distinguishes between left- and right-hand keys. If
     /// there is no translation, the function returns 0.
     /// </summary>
     MAPVK_VSC_TO_VK_EX = 0x03,

     /// <summary>
     /// Not currently documented
     /// </summary>
     MAPVK_VK_TO_VSC_EX = 0x04
}
```

## VB.NET User-Defined Types:
```cs
Const MAPVK_VK_TO_VSC = 0UI
Const MAPVK_VSC_TO_VK = 1UI
Const MAPVK_VK_TO_CHAR = 2UI
Const MAPVK_VSC_TO_VK_EX = 3UI
Const MAPVK_VK_TO_VSC_EX = 4UI
```

## VB.NET User-Defined Types:
```cs
''' <summary>
''' The set of valid MapTypes used in MapVirtualKey
''' </summary>
Enum MapVirtualKeyMapTypes
    ''' <summary>
    ''' uCode is a virtual-key code and is translated into a scan code.
    ''' If it is a virtual-key code that does not distinguish between left- and
    ''' right-hand keys, the left-hand scan code is returned.
    ''' If there is no translation, the function returns 0.
    ''' </summary>
    MAPVK_VK_TO_VSC = &H0

    ''' <summary>
    ''' uCode is a scan code and is translated into a virtual-key code that
    ''' does not distinguish between left- and right-hand keys. If there is no
    ''' translation, the function returns 0.
    ''' </summary>
    MAPVK_VSC_TO_VK = &H1

    ''' <summary>
    ''' uCode is a virtual-key code and is translated into an unshifted
    ''' character value in the low-order word of the return value. Dead keys (diacritics)
    ''' are indicated by setting the top bit of the return value. If there is no
    ''' translation, the function returns 0.
    ''' </summary>
    MAPVK_VK_TO_CHAR = &H2

    ''' <summary>
    ''' The uCode parameter is a scan code and is translated into a virtual-key code 
    ''' that distinguishes between left- and right-hand keys. If there is no translation, 
    ''' the function returns 0. 
    ''' </summary>
    MAPVK_VSC_TO_VK_EX = &H3

    ''' <summary>
    ''' The uCode parameter is a virtual-key code and is translated into a scan code. 
    ''' If it is a virtual-key code that does not distinguish between left- and right-hand keys,
    ''' the left-hand scan code is returned. If the scan code is an extended scan code,
    ''' the high byte of the uCode value can contain either 0xe0 or 0xe1 to specify the extended scan code.
    ''' If there is no translation, the function returns 0.
    ''' </summary>
    MAPVK_VK_TO_VSC_EX = &H4
End Enum
```
