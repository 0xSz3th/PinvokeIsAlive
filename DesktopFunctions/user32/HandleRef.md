
## C# Signature:
```cs
// NATIVE SUPPORT
HandleRef handle;
```

## Sample Code:
```cs
myFlawedFunction() {
    myObject o = new myObject();
    IntPtr hWnd = o.handle;

    //At this point the GC can run and 
    //collect myObject o since it's 
    //"not used" anymore.

    Win32.A_Function(hWnd);
   }

   myCorrectFunction() {
    myObject o = new myObject();
    IntPtr hWnd = o.handle;

    //The GC will not collect "o" here since 
    //there's a later reference to it.

    Win32.A_Function(new HandlRef(o, hWnd));
   }
```
