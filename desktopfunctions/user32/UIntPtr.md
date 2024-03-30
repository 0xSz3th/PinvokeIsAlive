//#include <cstring>
//void *memcpy( void *to, const void *from, size_t count );

[DllImport("msvcrt.dll", EntryPoint = "memcpy", CallingConvention = CallingConvention.Cdecl, SetLastError = false)]
public static extern IntPtr MemCopy(byte[] dest, byte[] src, UIntPtr count);

//Console Prints: 0 0 1
public static void CopyPrint()
{
    byte[] dest = new byte[] { 1, 1, 1 };
    byte[] src = new byte[] { 0, 0, 0 };
    UIntPtr count = new UIntPtr(2u);

    MemCopy(dest, src, count);

    for (int i = 0; i < dest.Length; i++)
    {
    Console.Write(dest[i] + " ");
    }
}
Click to read this page6/25/2010 2:17:25 PM - -90.152.60.34Click to read this page6/25/2010 2:17:25 PM - -90.152.60.34
