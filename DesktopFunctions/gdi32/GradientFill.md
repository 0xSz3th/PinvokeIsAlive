
## C# Signature:
```cs
[DllImport("gdi32.dll", EntryPoint = "GdiGradientFill", ExactSpelling = true)]
public static extern bool GradientFill(
    IntPtr hdc,           // handle to DC
    IntPtr pVertex,    // array of vertices
    uint dwNumVertex,     // number of vertices
    IntPtr pMesh,           // array of gradients
    uint dwNumMesh,       // size of gradient array
    uint dwMode           // gradient fill mode);
```

## VB Signature:
```cs
Declare Function GradientFill Lib "gdi32.dll" (TODO) As TODO
```
