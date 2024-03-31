
## C# Definition:
```cs
[Flags]
public enum SPIF
{
    None = 0x00,
    /// <summary>Writes the new system-wide parameter setting to the user profile.</summary>
    SPIF_UPDATEINIFILE = 0x01,
    /// <summary>Broadcasts the WM_SETTINGCHANGE message after updating the user profile.</summary>
    SPIF_SENDCHANGE = 0x02,
    /// <summary>Same as SPIF_SENDCHANGE.</summary>
    SPIF_SENDWININICHANGE = 0x02
}
```

## VB Definition:
```cs
<Flags> _
Enum SPIF
   None    =          &H0
   SPIF_UPDATEINIFILE =    &H1  ' Writes the new system-wide parameter setting to the user profile.
   SPIF_SENDCHANGE =       &H2  ' Broadcasts the WM_SETTINGCHANGE message after updating the user profile.
   SPIF_SENDWININICHANGE = &H2  ' Same as SPIF_SENDCHANGE.
End Enum
```
