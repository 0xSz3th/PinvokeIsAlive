[System.Runtime.InteropServices.DllImport("OLE32.DLL", EntryPoint = "CreateStreamOnHGlobal")] 
    // Create a COM stream from a pointer in unmanaged memory
    extern public static int CreateStreamOnHGlobal(IntPtr ptr, bool delete, out System.Runtime.InteropServices.ComTypes.IStream pOutStm);

    [DllImport("OLE32.DLL", ExactSpelling = true, PreserveSig = false)]
    private static extern void OleSaveToStream(IPersistStreamInit pPStm, IStream pStm);

       public int ByteSizeOfIPStreamInit(IPersistStreamInit pPersistStream)
       {
         int     iSzOfStreamInBytes=0;
         IntPtr  ptrIStream = IntPtr.Zero;
         IStream IPtrStream;

         if (CreateStreamOnHGlobal(ptrIStream, true, out IPtrStream) == 0)
         {
              OleSaveToStream(pPersistStream,IPtrStream);
              iSzOfStreamInBytes = IStreamSizeRead(IPtrStream);
         }
         return (iSzOfStreamInBytes * 2); // (Multiply By 2 because Int32 is 4 bytes; Use caution.)
       }

    public int IStreamSizeRead(IStream pOutStm)
    {
        pOutStm.Seek(0, 0, IntPtr.Zero);// Get size of the stream and read its contents to a byte array.
        System.Runtime.InteropServices.ComTypes.STATSTG fileinfo;
        pOutStm.Stat(out fileinfo, 0);
        byte[] data = new byte[fileinfo.cbSize];
        int sizeOfInt32 = Marshal.SizeOf(typeof(int));
        IntPtr pRead = Marshal.AllocHGlobal(sizeOfInt32);
        pOutStm.Read(data, data.Length, pRead);
        int read = Marshal.ReadInt32(pRead);
        Marshal.FreeHGlobal(pRead);
        return (data.Length);
    }
