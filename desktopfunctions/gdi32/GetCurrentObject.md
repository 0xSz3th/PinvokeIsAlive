
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern IntPtr GetCurrentObject(IntPtr hdc, uint uObjectType);
```

## User-Defined Types:
```cs
private enum ObjectType
{
OBJ_PEN = 1,
OBJ_BRUSH = 2,
OBJ_DC = 3,
OBJ_METADC = 4,
OBJ_PAL = 5,
OBJ_FONT = 6,
OBJ_BITMAP = 7,
OBJ_REGION = 8,
OBJ_METAFILE = 9,
OBJ_MEMDC = 10,
OBJ_EXTPEN = 11,
OBJ_ENHMETADC = 12,
OBJ_ENHMETAFILE = 13
}
```
