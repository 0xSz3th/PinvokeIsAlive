
## C# Signature:
```cs
[DllImport("ntdll.dll")]
public static extern int NtOpenDirectoryObject(
   out SafeFileHandle DirectoryHandle,
   uint DesiredAccess,
   ref OBJECT_ATTRIBUTES ObjectAttributes);
```

## Sample Code:
```cs
static void ObjectManagerTest()
{
   SafeFileHandle h;
   var attr = new OBJECT_ATTRIBUTES("\\", 0);
   var st = Win32.NtOpenDirectoryObject(
     out h, 1, ref attr);
   if (st < 0) return;

   var bufsz = 1024;
   var buf = Marshal.AllocHGlobal(bufsz);
   uint context = 0, len;
   for (; ; )
   {
     st = Win32.NtQueryDirectoryObject(h, buf, bufsz,
       true, context == 0, ref context, out len);
     if (st < 0) break;

     var odi = (OBJECT_DIRECTORY_INFORMATION)
       Marshal.PtrToStructure(buf, typeof(OBJECT_DIRECTORY_INFORMATION));
     System.Diagnostics.Debug.Print(
       "0x{0:X2}:{1,-25}{2}", context, odi.TypeName, odi.Name);
   }
   Marshal.FreeHGlobal(buf);
   h.Dispose();
}
```
