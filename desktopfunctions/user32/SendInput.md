
## C# Signature:
```cs
/// <summary>
   /// Synthesizes keystrokes, mouse motions, and button clicks.
   /// </summary>
   [DllImport("user32.dll")]
   internal static extern uint SendInput (uint nInputs, 
      [MarshalAs(UnmanagedType.LPArray), In] INPUT[] pInputs, 
      int cbSize);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll", SetLastError:=True)>
Friend Shared Function SendInput(<[In]()> ByVal nInput As UInt32,
  <[In](), MarshalAs(UnmanagedType.LPArray, ArraySubtype:=UnmanagedType.Struct, SizeParamindex:=0)> ByVal pInputs() As tagINPUT,
  <[In]()> ByVal cbInput As Int32) As UInt32
End Function
```

## VB Signature:
```cs
Private Declare Function SendInput Lib "user32.dll" (ByVal cInputs As Integer, ByRef pInputs As INPUT, ByVal cbSize As Integer) As Integer
```

## Sample Code:
```cs
var pInputs = new[]
   {
      new StructLib.INPUT()
      {
     type = EnumLib.INPUT_TYPE.INPUT_KEYBOARD,
     ki = new StructLib.KEYBDINPUT()
     {
        wScan = EnumLib.ScanCodeShort.KEY_S,
        wVk = EnumLib.VirtualKeyShort.KEY_S
     }
      },
      new StructLib.INPUT()
      {
     type = EnumLib.INPUT_TYPE.INPUT_KEYBOARD,
     ki = new StructLib.KEYBDINPUT()
     {
        wScan = EnumLib.ScanCodeShort.KEY_S,
        wVk = EnumLib.VirtualKeyShort.KEY_S,
        dwFlags = EnumLib.KEYEVENTF.KEYUP
     }
      },
      new StructLib.INPUT()
      {
     type = EnumLib.INPUT_TYPE.INPUT_KEYBOARD,
     ki = new StructLib.KEYBDINPUT()
     {
        wScan = EnumLib.ScanCodeShort.KEY_S,
        wVk = EnumLib.VirtualKeyShort.KEY_S
     }
      },
      new StructLib.INPUT()
      {
     type = EnumLib.INPUT_TYPE.INPUT_KEYBOARD,
     ki = new StructLib.KEYBDINPUT()
     {
        wScan = EnumLib.ScanCodeShort.KEY_S,
        wVk = EnumLib.VirtualKeyShort.KEY_S,
        dwFlags = EnumLib.KEYEVENTF.KEYUP
     }
      },
      new StructLib.INPUT()
      {
     type = EnumLib.INPUT_TYPE.INPUT_KEYBOARD,
     ki = new StructLib.KEYBDINPUT()
     {
        wScan = EnumLib.ScanCodeShort.KEY_S,
        wVk = EnumLib.VirtualKeyShort.KEY_S
     }
      },
      new StructLib.INPUT()
      {
     type = EnumLib.INPUT_TYPE.INPUT_KEYBOARD,
     ki = new StructLib.KEYBDINPUT()
     {
        wScan = EnumLib.ScanCodeShort.KEY_S,
        wVk = EnumLib.VirtualKeyShort.KEY_S,
        dwFlags = EnumLib.KEYEVENTF.KEYUP
     }
      }
   };

   var hWindow = Api.user32.FindWindow("notepad", null);
   Api.user32.SetForegroundWindow(hWindow);
   Thread.Sleep(2500);
   Api.user32.SendInput((uint)pInputs.Length, pInputs, StructLib.INPUT.Size);
```

## Sample Code:
```cs
[code]
   #region powershell yes it WORKS!! begin
   [testing.windows]::SetForegroundWindow( @( Get-Process notepad |? { $_.id -in @( get-wmiobject win32_process -filter "name='notepad.exe'" |% { if ( $_.getowner().user -eq $env:username ) { $_.processid } } ) } )[0].MainWindowHandle)

   $_inputList = New-Object 'Collections.Generic.List[Testing.Windows3+INPUT]'
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::KEY_S } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::KEY_S ; dwFlags = $( [Testing.Windows3+KEYEVENTF]::KEYUP ) } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::MENU  } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::KEY_E } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::MENU  ; dwFlags = $( [Testing.Windows3+KEYEVENTF]::KEYUP ) } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::KEY_E ; dwFlags = $( [Testing.Windows3+KEYEVENTF]::KEYUP ) } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::CONTROL  } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::KEY_F } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::CONTROL  ; dwFlags = $( [Testing.Windows3+KEYEVENTF]::KEYUP ) } ) } ) } ) )
   $_inputList.Add( $( New-Object Testing.Windows3+INPUT -Property @{ type = [Testing.Windows3+INPUT_TYPE]::KEYBOARD ; U = $( New-Object Testing.Windows3+InputUnion -Property @{ ki = $( New-Object Testing.Windows3+KEYBDINPUT -Property @{ wVk = [Testing.Windows3+VirtualKeyShort]::KEY_F ; dwFlags = $( [Testing.Windows3+KEYEVENTF]::KEYUP ) } ) } ) } ) )
   $_inputArray = $_inputList.ToArray()

   Start-Sleep 2 ; [Testing.Windows3]::SendInput($_inputArray.count, $_inputArray, [Runtime.InteropServices.marshal]::SizeOf($_inputArray[0]))
   #endregion powershell yes it WORKS!! end
   [/code]
```
