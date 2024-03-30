
## C# Signature:
```cs
[DllImport("ole32.dll")]
static extern int StgOpenStorageEx([MarshalAs(UnmanagedType.LPWStr)] string
   pwcsName, uint grfMode, uint stgfmt, uint grfAttrs, ref STGOPTIONS
   pStgOptions, IntPtr reserved2, [In] ref Guid riid,
   [MarshalAs(UnmanagedType.IUnknown)] out object ppObjectOpen);
```

## Alternative Managed API:
```cs
public static void ReadOSSFile(string fileName, XmlWriter writer)
    {
        int checkResult = StgIsStorageFile(fileName);
        Preconditions.RequireArgument(checkResult == 0, 
            "The specified file is not an OLE Structured Storage file.");

        StorageInfo storageRoot = GetStorageRoot(fileName);
        try
        {
            WriteStorage(storageRoot, fileName, writer);
        }
        finally
        {
            CloseStorageRoot(storageRoot);
        }
    }

    private static StorageInfo GetStorageRoot(string fileName)
    {
        StorageInfo storageRoot = (StorageInfo)InvokeStorageRootMethod(null, 
            "Open", fileName, FileMode.Open, FileAccess.Read, FileShare.Read);
        if (storageRoot == null)
        {
            Utilities.ThrowInvalidStateFmt("Unable to open \"{0}\" as a structured storage file.", fileName);
        }
        return storageRoot;
    }

    private static void CloseStorageRoot(StorageInfo storageRoot)
    {
        InvokeStorageRootMethod(storageRoot, "Close");
    }

    private static object InvokeStorageRootMethod(StorageInfo storageRoot, string methodName, params object[] methodArgs)
    {
        //We need the StorageRoot class to directly open an OSS file.  Unfortunately, it's internal.
        //So we'll have to use Reflection to access it.  This code was inspired by:
        //http://henbo.spaces.live.com/blog/cns!2E073207A544E12!200.entry
        //Note: In early WinFX CTPs the StorageRoot class was public because it was documented
        //here: http://msdn2.microsoft.com/en-us/library/aa480157.aspx

        Type storageRootType = typeof(StorageInfo).Assembly.GetType("System.IO.Packaging.StorageRoot", true, false);
        object result = storageRootType.InvokeMember(methodName,
            BindingFlags.Static | BindingFlags.Instance | BindingFlags.Public | BindingFlags.NonPublic | BindingFlags.InvokeMethod,
            null, storageRoot, methodArgs);
        return result;
    }

    private static void WriteStorage(StorageInfo storageInfo, string storageName, XmlWriter writer)
    {
        writer.WriteStartElement("storage");
        writer.WriteAttributeString("name", storageName);

        StorageInfo[] subStorages = storageInfo.GetSubStorages();
        foreach (StorageInfo subStorage in subStorages)
        {
            WriteStorage(subStorage, subStorage.Name, writer);
        }

        StreamInfo[] streams = storageInfo.GetStreams();
        foreach (StreamInfo stream in streams)
        {
            string hexData = ConvertStreamBytesToHex(stream);
            writer.WriteStartElement("stream");
            writer.WriteAttributeString("name", stream.Name);
            writer.WriteAttributeString("data", hexData);
            writer.WriteEndElement();
        }

        writer.WriteEndElement();
    }

    private static string ConvertStreamBytesToHex(StreamInfo streamInfo)
    {
        using (Stream streamReader = streamInfo.GetStream(FileMode.Open, FileAccess.Read))
        {
            StringBuilder sb = new StringBuilder();
            int currentRead;
            while ((currentRead = streamReader.ReadByte()) >= 0)
            {
                byte currentByte = (byte)currentRead;
                sb.AppendFormat("{0:X2}", currentByte);
            }
            return sb.ToString();
        }
    }

    [DllImport("ole32.dll", CharSet = CharSet.Unicode)]
    private static extern int StgIsStorageFile(string fileName);
```
