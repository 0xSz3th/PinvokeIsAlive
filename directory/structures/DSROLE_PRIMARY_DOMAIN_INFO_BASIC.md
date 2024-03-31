
## C# Definition:
```cs
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
    internal struct DSROLE_PRIMARY_DOMAIN_INFO_BASIC
    {
        public DSROLE_MACHINE_ROLE MachineRole;
        public uint Flags;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string DomainNameFlat;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string DomainNameDns;
        [MarshalAs(UnmanagedType.LPWStr)]
        public string DomainForestName;
        public Guid DomainGuid;
    }
```

## VB Definition:
```cs
Structure DSROLE_PRIMARY_DOMAIN_INFO_BASIC 
   Public TODO
End Structure
```
