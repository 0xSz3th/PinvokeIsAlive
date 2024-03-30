
## C# Signature:
```cs
[DllImport("advapi32.dll", EntryPoint = "TreeSetNamedSecurityInfoW", SetLastError = true, CharSet = CharSet.Unicode)]
static extern uint TreeSetNamedSecurityInfo(string pObjectName, SE_OBJECT_TYPE ObjectType, SecurityInformation SecurityInfo,
                        IntPtr pOwner, IntPtr pGroup, IntPtr pDacl, IntPtr pSacl, uint dwAction, 
                        TreeSetNamedSecurityProgress fnProgress, PROGRESS_INVOKE_SETTING ProgressInvokeSetting, IntPtr Args);

// callback function
public delegate void TreeSetNamedSecurityProgress(IntPtr pObjectName, uint Status, IntPtr pInvokeSetting, IntPtr Args, Boolean SecuritySet);
```

## User-Defined Types:
```cs
protected enum SE_OBJECT_TYPE
    {
        SE_UNKNOWN_OBJECT_TYPE = 0,
        SE_FILE_OBJECT,
        SE_SERVICE,
        SE_PRINTER,
        SE_REGISTRY_KEY,
        SE_LMSHARE,
        SE_KERNEL_OBJECT,
        SE_WINDOW_OBJECT,
        SE_DS_OBJECT,
        SE_DS_OBJECT_ALL,
        SE_PROVIDER_DEFINED_OBJECT,
        SE_WMIGUID_OBJECT,
        SE_REGISTRY_WOW64_32KEY
    }

    protected const uint TREE_SEC_INFO_SET   = 0x00000001;
    protected const uint TREE_SEC_INFO_RESET = 0x00000002;
    protected const uint TREE_SEC_INFO_RESET_KEEP_EXPLICIT = 0x00000003;

    public enum PROGRESS_INVOKE_SETTING 
    { 
        ProgressInvokeNever     = 1,
        ProgressInvokeEveryObject,
        ProgressInvokeOnError,
        ProgressCancelOperation,
        ProgressRetryOperation,
        ProgressInvokePrePostError
    }
```

## Sample Code:
```cs
Boolean retref, present;
    IntPtr pSidOwner = IntPtr.Zero;
    IntPtr pSidGroup = IntPtr.Zero;
    IntPtr pDacl = IntPtr.Zero;
    IntPtr pSacl = IntPtr.Zero;
    IntPtr pTemp = IntPtr.Zero;
    IntPtr pArgs = IntPtr.Zero;

    GetSecurityDescriptorGroup(pSecurityDescriptor, out pSidGroup , out retref);
    GetSecurityDescriptorOwner(pSecurityDescriptor, out pSidOwner, out retref));
    GetSecurityDescriptorDacl(pSecurityDescriptor, out present, out pDacl, out retref);
    GetSecurityDescriptorSacl(pSecurityDescriptor, out present, out pSacl, out retref);

    uint errorReturn = TreeSetNamedSecurityInfo(path, SE_OBJECT_TYPE.SE_FILE_OBJECT, si, pSidOwner, pSidGroup, pDacl, pSacl, TREE_SEC_INFO_SET, callback, PROGRESS_INVOKE_SETTING.ProgressInvokePrePostError, pArgs);
```

## Sample Code:
```cs
void TreeSetNamedSecurityProgress(IntPtr pObjectName, uint Status, IntPtr pInvokeSetting, IntPtr Args, Boolean SecuritySet)
    {
        if (bCancel)
        {
        pInvokeSetting = new IntPtr((int)Win32FileSystem.PROGRESS_INVOKE_SETTING.ProgressCancelOperation);
        return;
        }

        String temp = Marshal.PtrToStringAuto(pObjectName);
        if(!String.IsNullOrEmpty(temp))
        {
        String currentItem = temp;
        }
    }
```
