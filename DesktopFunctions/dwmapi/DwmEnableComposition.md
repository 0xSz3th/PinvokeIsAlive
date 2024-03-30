
## C# Signature:
```cs
[DllImport("dwmapi.dll", PreserveSig = false)]
      public static extern void DwmEnableComposition(CompositionAction uCompositionAction);

      [Flags]
      public enum CompositionAction : uint
      {
     /// <summary>
     /// To enable DWM composition
     /// </summary>
     DWM_EC_DISABLECOMPOSITION = 0,
     /// <summary>
     /// To disable composition.
     /// </summary>
     DWM_EC_ENABLECOMPOSITION = 1
      }
```

## VB Signature:
```cs
<DllImport("dwmapi.dll")> _
    Public Shared Sub DwmEnableComposition(ByVal uCompositionAction As CompositionAction)
    End Sub

    Public Enum CompositionAction As UInteger
    DWM_EC_DISABLECOMPOSITION = 0
    DWM_EC_ENABLECOMPOSITION = 1
    End Enum
```

## Sample Code C#:
```cs
public static void DisableAero(bool disable)
      {
     if (disable)
        DwmEnableComposition(CompositionAction.DWM_EC_DISABLECOMPOSITION);
     else
        DwmEnableComposition(CompositionAction.DWM_EC_ENABLECOMPOSITION);
      }
```
