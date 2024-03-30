
## C# Signature:
```cs
[DllImport("gdiplus.dll", CharSet=CharSet.Unicode)]
public static extern int GdipLoadImageFromFile(string filename, out IntPtr image);
```

## Sample Code:
```cs
public class FastImageGdiPlus 
    {
        [DllImport("gdiplus.dll", CharSet=CharSet.Unicode)]
        public static extern int GdipLoadImageFromFile(string filename, out IntPtr image);

        private FastImageGdiPlus() 
        {
        }

        private static Type imageType = typeof(System.Drawing.Bitmap);

        [SecurityPermission(SecurityAction.Demand, Flags = SecurityPermissionFlag.UnmanagedCode)]
        internal static Image FastFromFile(string filename) 
        {
            try
            {
                filename = Path.GetFullPath(filename);
                IntPtr loadingImage = IntPtr.Zero;

                // We are not using ICM at all, fudge that, this should be FAAAAAST!
                if ( GdipLoadImageFromFile(filename, out loadingImage) != 0 ) 
                {
                    throw new Exception("GDI+ threw a status error code.");
                }

                return (Bitmap) imageType.InvokeMember("FromGDIplus", BindingFlags.NonPublic | BindingFlags.Static | BindingFlags.InvokeMethod, null, null, new object[] { loadingImage });
            }
            catch(SecurityException)
            {
                return Image.FromFile(filename);
            }
        }
    }
```
