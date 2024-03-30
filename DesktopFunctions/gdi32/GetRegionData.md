
## C# Signature:
```cs
[DllImport("gdi32.dll")]
static extern int GetRegionData(IntPtr hRgn, uint dwCount, IntPtr lpRgnData);
```

## Sample Code:
```cs
using System;
  using System.Runtime.InteropServices;

  // this should be defined somewhere in a class
  const int RDH_RECTANGLES = 1;

  unsafe RECT[] RectsFromRegion(IntPtr hRgn)
  {
    RECT [] rects = null;

    // First we call GetRegionData() with a null buffer.
    // The return from this call should be the size of buffer
    // we need to allocate in order to receive the data. 
    int dataSize = GetRegionData(hRgn, 0, IntPtr.Zero);

    if (dataSize != 0)
    {
     IntPtr bytes = IntPtr.Zero;

      // Allocate as much space as the GetRegionData call 
      // said was needed
      bytes = Marshal.AllocCoTaskMem(dataSize);

      // Now, make the call again to actually get the data
      int retValue = GetRegionData(hRgn, dataSize, bytes);

      // From here on out, we have the data in a buffer, and we 
      // just need to convert it into a form that is more useful
      // Since pointers are used, this whole routine is 'unsafe'
      // It's a small sacrifice to make in order to get this to work.
      // [RBS] Added missing second pointer identifier
      RGNDATAHEADER * header = (RGNDATAHEADER*)bytes;

      if (header->iType == RDH_RECTANGLES)
      {
    rects = new RECT[header->nCount];

    // The rectangle data follows the header, so we offset the specified
    // header size and start reading rectangles.
    int rectOffset = header->dwSize;
    for (int i=0; i < header->nCount; i++)
    {
      // simple assignment from the buffer to our array of rectangles
      // will give us what we want.
      rects[i] = *((RECT *)((byte *)bytes+rectOffset+(Marshal.SizeOf(typeof(RECT)) *i)));
    }
      }

    }

    // Return the rectangles
    return rects;

  }
```
