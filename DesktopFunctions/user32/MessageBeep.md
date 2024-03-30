
## C# Signature:
```cs
[DllImport("user32.dll")]
[return: MarshalAs(UnmanagedType.Bool)]
static extern bool MessageBeep(beepType uType);
```

## VB.NET Signature:
```cs
<DllImport("user32.dll")> _
Private Shared Function MessageBeep(ByVal uType As beepType) As Boolean
End Function
```

## dylan.NET Signiture:
```cs
dllimport user32.dll
callconv winapi
charset auto
method public static pinvokeimpl boolean MessageBeep(var uType as integer)
setattr param|0 marshalas Bool
```

## Sample Code:
```cs
/// <summary>
    /// Enum type that enables intellisense on the private <see cref="Beep"/> method.
    /// </summary>
    /// <remarks>
    /// Used by the public Beep <see cref="Beep"/></remarks>
    public enum beepType : uint
    {
        /// <summary>
        /// A simple windows beep
        /// </summary>            
        SimpleBeep  = 0xFFFFFFFF,
        /// <summary>
        /// A standard windows OK beep
        /// </summary>
        OK    = 0x00,
        /// <summary>
        /// A standard windows Question beep
        /// </summary>
        Question  = 0x20,
        /// <summary>
        /// A standard windows Exclamation beep
        /// </summary>
        Exclamation  = 0x30,
        /// <summary>
        /// A standard windows Asterisk beep
        /// </summary>
        Asterisk  = 0x40,
    }

    [DllImport("User32.dll", ExactSpelling=true)]
    private static extern bool MessageBeep(uint type);

    /// <summary>
    /// Method to call interop for system beep
    /// </summary>
    /// <remarks>Calls Windows to make computer beep</remarks>
    /// <param name="type">The kind of beep you would like to hear</param>
    public static void beep(beepType type)
    {
        MessageBeep((uint)type);
    }
```

## Sample Code:
```cs
class Class1
    {
        public enum beepType
        {
            /// <summary>
            /// A simple windows beep
            /// </summary>            
            SimpleBeep  = -1,
            /// <summary>
            /// A standard windows OK beep
            /// </summary>
            OK    = 0x00,
            /// <summary>
            /// A standard windows Question beep
            /// </summary>
            Question  = 0x20,
            /// <summary>
            /// A standard windows Exclamation beep
            /// </summary>
            Exclamation  = 0x30,
            /// <summary>
            /// A standard windows Asterisk beep
            /// </summary>
            Asterisk  = 0x40,
        }
        [DllImport("User32.dll", ExactSpelling=true)]
        private static extern bool MessageBeep(uint type);

        static void Main(string[] args)
        {
            Class1.beep(beepType.Asterisk);
            Thread.Sleep(1000);
            Class1.beep(beepType.Exclamation);
            Thread.Sleep(1000);
            Class1.beep(beepType.OK);
            Thread.Sleep(1000);
            Class1.beep(beepType.Question);
            Thread.Sleep(1000);
            Class1.beep(beepType.SimpleBeep);
        }
        public static void beep(beepType type)
        {
            MessageBeep((uint)type);
        }

        }
    }
```
