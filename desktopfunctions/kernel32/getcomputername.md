
## C# Signature:
```cs
[DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
static extern bool GetComputerNameEx(COMPUTER_NAME_FORMAT NameType,
   StringBuilder lpBuffer, ref uint lpnSize);
```

## VB.Net Signature:
```cs
<DllImport("kernel32.dll", CharSet:=CharSet.Auto, SetLastError:=True)> _
Private Shared Function GetComputerNameEx(ByVal NameType As COMPUTER_NAME_FORMAT, ByVal lpBuffer As StringBuilder, ByRef lpnSize As UInt32) As Boolean
End Function
```

## Sample Code:
```cs
class Class1
    {
    enum COMPUTER_NAME_FORMAT
    {
        ComputerNameNetBIOS,
        ComputerNameDnsHostname,
        ComputerNameDnsDomain,
        ComputerNameDnsFullyQualified,
        ComputerNamePhysicalNetBIOS,
        ComputerNamePhysicalDnsHostname,
        ComputerNamePhysicalDnsDomain,
        ComputerNamePhysicalDnsFullyQualified
    }

    [DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
    static extern bool GetComputerNameEx(COMPUTER_NAME_FORMAT NameType,
        StringBuilder lpBuffer, ref uint lpnSize);

    [STAThread]
    static void Main(string[] args)
    {
        bool success;
        StringBuilder name = new StringBuilder(260);
        uint size = 260;
        success = GetComputerNameEx(COMPUTER_NAME_FORMAT.ComputerNameDnsDomain, name, ref size);
        Console.WriteLine(name.ToString());
    }
     }
```

## Sample Code:
```cs
$signature = @"
      using System;
      using System.Text;
      using System.Runtime.InteropServices;
      namespace Test_Namespace{
    public enum COMPUTER_NAME_FORMAT
    {
        ComputerNameNetBIOS,
        ComputerNameDnsHostname,
        ComputerNameDnsDomain,
        ComputerNameDnsFullyQualified,
        ComputerNamePhysicalNetBIOS,
        ComputerNamePhysicalDnsHostname,
        ComputerNamePhysicalDnsDomain,
        ComputerNamePhysicalDnsFullyQualified
    }
    public class Test_class{
        [DllImport("kernel32.dll", SetLastError=true, CharSet=CharSet.Auto)]
        public static extern bool GetComputerNameEx(COMPUTER_NAME_FORMAT NameType,
          StringBuilder lpBuffer, ref uint lpnSize);
    }       
    }    
    "@
    Add-Type -TypeDefinition $signature -PassThru
    $size = 64
    # way 2 to declare string builder
    $str_builder_obj = [System.Text.StringBuilder]::new($size)
    # run the method
    [Test_Namespace.Test_class]::GetComputerNameEx([Test_Namespace.COMPUTER_NAME_FORMAT]::ComputerNameDnsDomain, $str_builder_obj, [ref]$size)
    # view the contents
    $str_builder_obj.ToString()
```
