
## C# Signature:
```cs
static unsafe void InitializeObjectAttributes(out OBJECT_ATTRIBUTES InitializedAttributes, ref UNICODE_STRING ObjectName, uint Attributes, IntPtr RootDirectory, IntPtr SecurityDescriptor)
    {
        fixed (UNICODE_STRING* objectNamePtr = &ObjectName)
        {
            InitializedAttributes.Length = sizeof(OBJECT_ATTRIBUTES);
            InitializedAttributes.RootDirectory = RootDirectory;
            InitializedAttributes.Attributes = Attributes;
            InitializedAttributes.ObjectName = (IntPtr)objectNamePtr;
            InitializedAttributes.SecurityDescriptor = SecurityDescriptor;
            InitializedAttributes.SecurityQualityOfService = NULL;
        }
    }
```

## VB Signature:
```cs
Declare Function InitializeObjectAttributes Lib "ntdll.dll" (TODO) As TODO
```
