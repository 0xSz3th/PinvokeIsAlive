
## C# Signature:
```cs
[DllImport("advapi32.dll", CharSet = CharSet.Auto)]
  public static extern int RegOpenKeyEx(
    UIntPtr hKey,
    string subKey,
    int ulOptions,
    int samDesired,
    out UIntPtr hkResult);
```

## VB Signature:
```cs
Declare Auto Function RegOpenKeyEx Lib "advapi32.dll"  (
   ByVal hKey As IntPtr,
   ByVal lpSubKey As String,
   ByVal ulOptions As Integer,
   ByVal samDesired As Integer,
   ByRef phkResult As Integer
) As Integer
```

## Notes:
```cs
public static UIntPtr HKEY_LOCAL_MACHINE = new UIntPtr(0x80000002u);
public static UIntPtr HKEY_CURRENT_USER  = new UIntPtr(0x80000001u);
```

## Notes:
```cs
Const KEY_QUERY_VALUE = &H1
Const KEY_SET_VALUE = &H2
Const KEY_CREATE_SUB_KEY = &H4
Const KEY_ENUMERATE_SUB_KEYS = &H8
Const KEY_NOTIFY = &H10
Const KEY_CREATE_LINK = &H20
Const KEY_WOW64_32KEY = &H200
Const KEY_WOW64_64KEY = &H100
Const KEY_WOW64_RES = &H300
```

## Tips & Tricks:
```cs
ReadRegKey(HKEY_LOCAL_MACHINE, @"Software\SomeCompany\OurProduct", "InstalledVersion"); 

   works but something like

   ReadRegKey(_getRegistryKeyHandle(Registry.LocalMachine.CreateSubKey( @"Software\SomeCompany")),"OurProduct", "InstalledVersion"); 

   does not actually get the 64 bit key if its a 32 bit app.
```

## Sample Code (VB):
```cs
Public Enum RegWow64Options As Integer
   None = 0
   KEY_WOW64_64KEY = &H100
   KEY_WOW64_32KEY = &H200
End Enum

Public Enum RegistryRights As Integer
   ReadKey = 131097
   WriteKey = 131078
End Enum

' overloaded, see below
Public Function OpenSubKey(ByVal Name As String) As RegistryKey
   Return OpenSubKey(Name, False, RegWow64Options.None)
End Function

' overloaded, see below
Public Function OpenSubKey(ByVal Name As String, ByVal Writeable As Boolean) As RegistryKey
   Return OpenSubKey(Name, Writeable, RegWow64Options.None)
End Function

' open a SubKey
Public Function OpenSubKey(ByVal Name As String, ByVal Writeable As Boolean, ByVal Options As RegWow64Options) As RegistryKey
   Dim ret, Rights As Integer
   Dim hSubKey As IntPtr

   ' quick sanity check
   If hKey.Equals(IntPtr.Zero) Then
     Throw New ApplicationException("Cannot access a closed registry key")
   End If

   Rights = RegistryRights.ReadKey
   If Writeable Then
     Rights = RegistryRights.WriteKey
   End If

   ' Ignore the 64-bit flags when running from <= Win2k
   If CDbl(Environment.OSVersion.Version.Major & "." & Environment.OSVersion.Version.Minor) <= 5.0 Then
     Options = RegWow64Options.None
   End If

   ret = RegOpenKeyEx(hKey, Name, 0, Rights Or Options, hSubKey)
   If ret <> 0 Then
     Return Nothing
   End If

   Dim ans As New RegistryKey
   ans.hKey = hSubKey
   ans.RegKeyName = Name
   ans.IsRootHive = False
   Return ans
End Function
```

## Sample Code (VB) to convert an IntPtr to a RegistryKey
```cs
Public Shared Function PointerToRegistryKey(ByVal hKey As IntPtr, ByVal writable As Boolean, ByVal ownsHandle As Boolean) As RegistryKey
    ' Create a SafeHandles.SafeRegistryHandle from this pointer - this is a private class
    Dim privateConstructors = Reflection.BindingFlags.Instance Or Reflection.BindingFlags.NonPublic
    Dim safeRegistryHandleType = GetType(SafeHandles.SafeHandleZeroOrMinusOneIsInvalid).Assembly.GetType("Microsoft.Win32.SafeHandles.SafeRegistryHandle")
    Dim safeRegistryHandleConstructorTypes As System.Type() = {GetType(IntPtr), GetType(Boolean)}
    Dim safeRegistryHandleConstructor = safeRegistryHandleType.GetConstructor(privateConstructors, Nothing, safeRegistryHandleConstructorTypes, Nothing)
    Dim safeHandle = safeRegistryHandleConstructor.Invoke(New Object() {hKey, ownsHandle})

    ' Create a new Registry key using the private constructor using the safeHandle - this should then behave like a .NET natively opened handle and disposed of correctly
    Dim registryKeyType = GetType(RegistryKey)
    Dim registryKeyConstructorTypes As System.Type() = {safeRegistryHandleType, GetType(Boolean)}
    Dim registryKeyConstructor = registryKeyType.GetConstructor(privateConstructors, Nothing, registryKeyConstructorTypes, Nothing)
    Dim result = DirectCast(registryKeyConstructor.Invoke(New Object() {safeHandle, writable}), RegistryKey)
    Return result
End Function
```

## Sample Code (C#) to read a string value
```cs
string example = ReadRegKey(HKEY_LOCAL_MACHINE, @"Software\SomeCompany\OurProduct", "InstalledVersion");

private static string ReadRegKey(UIntPtr rootKey, string keyPath, string valueName)
{
   if (RegOpenKeyEx(rootKey, keyPath, 0, KEY_READ, out hKey) == 0)
   {
      uint size = 1024;
      uint type;
      string keyValue = null;
      StringBuilder keyBuffer = new StringBuilder((int)size);

      if (RegQueryValueEx(hKey, valueName, IntPtr.Zero, out type, keyBuffer, ref size) == 0)
          keyValue = keyBuffer.ToString();

      RegCloseKey(hKey);

      return(keyValue);
  }

  return(null);  // Return null if the value could not be read
```

## Working VB.net Code
```cs
' Basis from http://blogs.msdn.com/cumgranosalis/archive/2005/12/09/Win64RegistryPart1.aspx
    Private Function GetRegistryKeyHandle(ByVal RegisteryKey As Microsoft.Win32.RegistryKey) As System.IntPtr
    Dim Type As System.Type = System.Type.GetType("Microsoft.Win32.RegistryKey")
    Dim Info As System.Reflection.FieldInfo = Type.GetField("hkey", System.Reflection.BindingFlags.NonPublic Or System.Reflection.BindingFlags.Instance)

    Dim Handle As System.Runtime.InteropServices.SafeHandle = CType(Info.GetValue(RegisteryKey), System.Runtime.InteropServices.SafeHandle)
    Dim RealHandle As System.IntPtr = Handle.DangerousGetHandle

    Return Handle.DangerousGetHandle
    End Function

    ' Basis from: http://www.pinvoke.net/default.aspx/advapi32/RegOpenKeyEx.html
    Public Enum RegWow64Options As System.Int32
    None = 0
    KEY_WOW64_64KEY = &H100
    KEY_WOW64_32KEY = &H200
    End Enum

    Private Enum RegistryRights As System.Int32
    ReadKey = 131097
    WriteKey = 131078
    End Enum

    Private Declare Auto Function RegOpenKeyEx Lib "advapi32.dll" (ByVal hKey As System.IntPtr, ByVal lpSubKey As System.String, ByVal ulOptions As System.Int32, ByVal samDesired As System.Int32, ByRef phkResult As System.Int32) As System.Int32

    Public Function OpenSubKey(ByVal ParentKey As Microsoft.Win32.RegistryKey, ByVal SubKeyName As String, ByVal Writeable As Boolean, ByVal Options As RegWow64Options) As Microsoft.Win32.RegistryKey
    If ParentKey Is Nothing OrElse GetRegistryKeyHandle(ParentKey).Equals(System.IntPtr.Zero) Then
        Throw New System.Exception("OpenSubKey: Parent key is not open")
    End If

    Dim Rights As System.Int32 = RegistryRights.ReadKey
    If Writeable Then
        Rights = RegistryRights.WriteKey
    End If

    Dim SubKeyHandle As System.Int32
    Dim Result As System.Int32 = RegOpenKeyEx(GetRegistryKeyHandle(ParentKey), SubKeyName, 0, Rights Or Options, SubKeyHandle)
    If Result <> 0 Then
        Dim W32ex As New System.ComponentModel.Win32Exception()
        Throw New System.Exception("OpenSubKey: Exception encountered opening key", W32ex)
    End If

    Return PointerToRegistryKey(CType(SubKeyHandle, System.IntPtr), Writeable, False)
    End Function

    Private Function PointerToRegistryKey(ByVal hKey As System.IntPtr, ByVal writable As Boolean, ByVal ownsHandle As Boolean) As Microsoft.Win32.RegistryKey
    ' Create a SafeHandles.SafeRegistryHandle from this pointer - this is a private class
    Dim privateConstructors As System.Reflection.BindingFlags = System.Reflection.BindingFlags.Instance Or System.Reflection.BindingFlags.NonPublic
    Dim safeRegistryHandleType As System.Type = GetType(Microsoft.Win32.SafeHandles.SafeHandleZeroOrMinusOneIsInvalid).Assembly.GetType("Microsoft.Win32.SafeHandles.SafeRegistryHandle")
    Dim safeRegistryHandleConstructorTypes As System.Type() = {GetType(System.IntPtr), GetType(System.Boolean)}
    Dim safeRegistryHandleConstructor As System.Reflection.ConstructorInfo = safeRegistryHandleType.GetConstructor(privateConstructors, Nothing, safeRegistryHandleConstructorTypes, Nothing)
    Dim safeHandle As System.Object = safeRegistryHandleConstructor.Invoke(New System.Object() {hKey, ownsHandle})

    ' Create a new Registry key using the private constructor using the safeHandle - this should then behave like a .NET natively opened handle and disposed of correctly
    Dim registryKeyType As System.Type = GetType(Microsoft.Win32.RegistryKey)
    Dim registryKeyConstructorTypes As System.Type() = {safeRegistryHandleType, GetType(System.Boolean)}
    Dim registryKeyConstructor As System.Reflection.ConstructorInfo = registryKeyType.GetConstructor(privateConstructors, Nothing, registryKeyConstructorTypes, Nothing)
    Dim result As Microsoft.Win32.RegistryKey = DirectCast(registryKeyConstructor.Invoke(New Object() {safeHandle, writable}), Microsoft.Win32.RegistryKey)
    Return result
    End Function
```

## Working VB.net Code
```cs
Dim Config As Microsoft.Win32.RegistryKey = Nothing
        If Is64Bit() Then
        Config = OpenSubKey(Microsoft.Win32.Registry.LocalMachine, "SOFTWARE\" & BaseName, False, RegWow64Options.KEY_WOW64_64KEY)
        Else
        Config = Microsoft.Win32.Registry.LocalMachine.OpenSubKey("SOFTWARE\" & BaseName, False)
        End If
```

## Working C#.NET Code + Usage
```cs
enum RegWow64Options
    {
        None = 0,
        KEY_WOW64_64KEY = 0x0100,
        KEY_WOW64_32KEY = 0x0200
    }

    enum RegistryRights
    {
        ReadKey = 131097,
        WriteKey = 131078
    }

    /// <summary>
    /// Open a registry key using the Wow64 node instead of the default 32-bit node.
    /// </summary>
    /// <param name="parentKey">Parent key to the key to be opened.</param>
    /// <param name="subKeyName">Name of the key to be opened</param>
    /// <param name="writable">Whether or not this key is writable</param>
    /// <param name="options">32-bit node or 64-bit node</param>
    /// <returns></returns>
    RegistryKey _openSubKey(RegistryKey parentKey, string subKeyName, bool writable, RegWow64Options options)
    {
        //Sanity check
        if (parentKey == null || _getRegistryKeyHandle(parentKey) == IntPtr.Zero)
        {
            return null;
        }

        //Set rights
        int rights = (int)RegistryRights.ReadKey;
        if (writable)
            rights = (int)RegistryRights.WriteKey;

        //Call the native function >.<
        int subKeyHandle, result = RegOpenKeyEx(_getRegistryKeyHandle(parentKey), subKeyName, 0, rights | (int)options, out subKeyHandle);

        //If we errored, throw an exception
        if (result != 0)
        {
            throw new Exception("Exception encountered opening registry key.", new System.ComponentModel.Win32Exception(result));
        }

        //Get the key represented by the pointer returned by RegOpenKeyEx
        RegistryKey subKey = _pointerToRegistryKey((IntPtr)subKeyHandle, writable, false);
        return subKey;
    }

    /// <summary>
    /// Get a pointer to a registry key.
    /// </summary>
    /// <param name="registryKey">Registry key to obtain the pointer of.</param>
    /// <returns>Pointer to the given registry key.</returns>
    IntPtr _getRegistryKeyHandle(RegistryKey registryKey)
    {
        //Get the type of the RegistryKey
        Type registryKeyType = typeof(RegistryKey);

        //Get the FieldInfo of the 'hkey' member of RegistryKey
        System.Reflection.FieldInfo fieldInfo = 
            registryKeyType.GetField("hkey", System.Reflection.BindingFlags.NonPublic | System.Reflection.BindingFlags.Instance);

        //Get the handle held by hkey
        SafeHandle handle = (SafeHandle)fieldInfo.GetValue(registryKey);

        //Get the unsafe handle
        IntPtr dangerousHandle = handle.DangerousGetHandle();
        return dangerousHandle;
    }

    /// <summary>
    /// Get a registry key from a pointer.
    /// </summary>
    /// <param name="hKey">Pointer to the registry key</param>
    /// <param name="writable">Whether or not the key is writable.</param>
    /// <param name="ownsHandle">Whether or not we own the handle.</param>
    /// <returns>Registry key pointed to by the given pointer.</returns>
    RegistryKey _pointerToRegistryKey(IntPtr hKey, bool writable, bool ownsHandle)
    {
        //Get the BindingFlags for private contructors
        System.Reflection.BindingFlags privateConstructors = System.Reflection.BindingFlags.Instance | System.Reflection.BindingFlags.NonPublic;

        //Get the Type for the SafeRegistryHandle
        Type safeRegistryHandleType = 
            typeof(Microsoft.Win32.SafeHandles.SafeHandleZeroOrMinusOneIsInvalid).Assembly.GetType("Microsoft.Win32.SafeHandles.SafeRegistryHandle");

        //Get the array of types matching the args of the ctor we want
        Type[] safeRegistryHandleCtorTypes = new Type[] { typeof(IntPtr), typeof(bool) };

        //Get the constructorinfo for our object
        System.Reflection.ConstructorInfo safeRegistryHandleCtorInfo = safeRegistryHandleType.GetConstructor(
            privateConstructors, null, safeRegistryHandleCtorTypes, null);

        //Invoke the constructor, getting us a SafeRegistryHandle
        Object safeHandle = safeRegistryHandleCtorInfo.Invoke(new Object[] { hKey, ownsHandle });

        //Get the type of a RegistryKey
        Type registryKeyType = typeof(RegistryKey);

        //Get the array of types matching the args of the ctor we want
        Type[] registryKeyConstructorTypes = new Type[] { safeRegistryHandleType, typeof(bool) };

        //Get the constructorinfo for our object
        System.Reflection.ConstructorInfo registryKeyCtorInfo = registryKeyType.GetConstructor(
            privateConstructors, null, registryKeyConstructorTypes, null);

        //Invoke the constructor, getting us a RegistryKey
        RegistryKey resultKey = (RegistryKey)registryKeyCtorInfo.Invoke(new Object[] { safeHandle, writable });

        //return the resulting key
        return resultKey;
    }

    [DllImport("advapi32.dll", CharSet = CharSet.Auto)]
    public static extern int RegOpenKeyEx(IntPtr hKey, string subKey, int ulOptions, int samDesired, out int phkResult);
```

## Working C#.NET Code + Usage
```cs
string _getWindowsProductId()
    {
        RegistryKey currentVersion =
            Registry.LocalMachine.OpenSubKey("SOFTWARE").OpenSubKey("Microsoft").OpenSubKey("Windows NT").OpenSubKey("CurrentVersion");

        string productID = (string)currentVersion.GetValue("ProductId") ?? string.Empty;

        if (productID == string.Empty)
        {
            RegistryKey software = _openSubKey(Registry.LocalMachine, "SOFTWARE", false, RegWow64Options.KEY_WOW64_64KEY);
            RegistryKey microsoft = _openSubKey(software, "Microsoft", false, RegWow64Options.KEY_WOW64_64KEY);
            RegistryKey windowsNT = _openSubKey(microsoft, "Windows NT", false, RegWow64Options.KEY_WOW64_64KEY);
            currentVersion = _openSubKey(windowsNT, "CurrentVersion", false, RegWow64Options.KEY_WOW64_64KEY);
            productID = (string)currentVersion.GetValue("ProductId") ?? string.Empty;
        }
        return productID;
    }
```

## Microsoft .NET Framework 4.0
```cs
' HKLM\SOFTWARE
    Dim regkey As Microsoft.Win32.RegistryKey = Microsoft.Win32.RegistryKey.OpenBaseKey(Microsoft.Win32.RegistryHive.LocalMachine, Microsoft.Win32.RegistryView.Registry32).OpenSubKey("SOFTWARE")
```

## Microsoft .NET Framework 4.0
```cs
' HKLM\SOFTWARE
    Microsoft.Win32.RegistryKey regkey = Microsoft.Win32.RegistryKey.OpenBaseKey(Microsoft.Win32.RegistryHive.LocalMachine, Microsoft.Win32.RegistryView.Registry32).OpenSubKey("SOFTWARE")
```

## Microsoft .NET Framework 4.0 - how to get the above sample running
```cs
/// <summary>
    /// Get a registry key from a pointer.
    /// </summary>
    /// <param name="hKey">Pointer to the registry key</param>
    /// <param name="writable">Whether or not the key is writable.</param>
    /// <param name="ownsHandle">Whether or not we own the handle.</param>
    /// <returns>Registry key pointed to by the given pointer.</returns>
    RegistryKey _pointerToRegistryKey(IntPtr hKey, bool writable, bool ownsHandle)
    {
        //Get the BindingFlags for public contructors
        System.Reflection.BindingFlags publicConstructors = System.Reflection.BindingFlags.Instance | System.Reflection.BindingFlags.Public; // NOTE: this has been changed since .NET 3.5 (was 'private').

        //Get the Type for the SafeRegistryHandle
        Type safeRegistryHandleType = 
            typeof(Microsoft.Win32.SafeHandles.SafeHandleZeroOrMinusOneIsInvalid).Assembly.GetType("Microsoft.Win32.SafeHandles.SafeRegistryHandle");

        //Get the array of types matching the args of the ctor we want
        Type[] safeRegistryHandleCtorTypes = new Type[] { typeof(IntPtr), typeof(bool) };

        //Get the constructorinfo for our object
        System.Reflection.ConstructorInfo safeRegistryHandleCtorInfo = safeRegistryHandleType.GetConstructor(
            publicConstructors, null, safeRegistryHandleCtorTypes, null);

        //Get the SafeRegistryHandle
        Microsoft.Win32.SafeHandles.SafeRegistryHandle safeHandle = (Microsoft.Win32.SafeHandles.SafeRegistryHandle)safeRegistryHandleCtorInfo.Invoke(new Object[] { hKey, ownsHandle });

        //Get the RegistryKey
        Microsoft.Win32.RegistryKey resultKey = Microsoft.Win32.RegistryKey.FromHandle(safeHandle); // ONLY possible under .NET 4.0! In .NET 3.5 there is no .FromHandle Method available!

        //return the resulting key
        return resultKey;
    }
An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29Click to read this page6/25/2010 2:17:25 PM - -90.152.60.34An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29Click to read this page6/25/2010 2:17:25 PM - -90.152.60.34TODO - a short description3/16/2007 8:11:30 AM - -61.11.98.124The FormatMessage API12/27/2020 2:24:15 AM - -84.110.53.106Opens the specified registry key6/12/2012 9:11:53 AM - born2c0de@dreamincode.net-125.99.58.184An IntPtr is a pointer to a memory location (unmanaged) that adapts to the platform it is running on (64-bit, etc.) UNLIKE a standard int/Integer. You should always use this type for unmanaged calls that require it, even though an int will appear to work on your development machine.1/13/2008 4:00:13 AM - Damon Carr-72.43.165.29
```
