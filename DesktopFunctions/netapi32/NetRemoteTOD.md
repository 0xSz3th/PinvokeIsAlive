
## C# Signature:
```cs
[DllImport("Netapi32.dll", CharSet=CharSet.Unicode)]
static extern int NetRemoteTOD(string UncServerName, ref IntPtr BufferPtr);
```

## VB Signature:
```cs
<DllImport("netapi32", CharSet:=CharSet.Unicode)> Function NetRemoteTOD( _
    ByVal UncServerName As String, ByRef BufferPtr As IntPtr) As Integer
    End Function!!!!User-Defined Types:
```

## Sample Code:
```cs
public class GetNetRemoteTOD
{
        #region API
        [DllImport( "netapi32.dll" , EntryPoint="NetRemoteTOD",  SetLastError=true,
        CharSet=CharSet.Unicode, ExactSpelling=true,
        CallingConvention=CallingConvention.StdCall)] private static extern int NetRemoteTOD(string UncServerName, ref IntPtr BufferPtr);
        [DllImport( "netapi32.dll")] private static extern void NetApiBufferFree(IntPtr bufptr);

        [StructLayout(LayoutKind.Sequential)]
        public struct structTIME_OF_DAY_INFO
        {
            public int itod_elapsedt;
                public int itod_msecs;
                public int itod_hours;
                public int itod_mins;
                public int itod_secs;
                public int itod_hunds;
                public int itod_timezone;
                public int itod_tinterval;
                public int itod_day;
                public int itod_month;
                public int itod_year;
            public int itod_weekday;
        }
        #endregion
```

## Sample Code:
```cs
#region Core functions
        public int [] xNetRemoteTOD( string ServerName )
         {
            structTIME_OF_DAY_INFO result = new structTIME_OF_DAY_INFO();
            IntPtr pintBuffer = IntPtr.Zero;
            int[] TOD_INFO = new int[12];

            // Get the time of day.
            int pintError = NetRemoteTOD(ServerName, ref pintBuffer);
            if ( pintError > 0 ) { throw new System.ComponentModel.Win32Exception ( pintError ); }

            // Get the structure.
            result = (structTIME_OF_DAY_INFO)Marshal.PtrToStructure(pintBuffer, typeof(structTIME_OF_DAY_INFO));

            TOD_INFO[0]  = result.itod_elapsedt;
                TOD_INFO[1]  = result.itod_msecs;
                TOD_INFO[2]  = result.itod_hours;
                TOD_INFO[3]  = result.itod_mins;
                TOD_INFO[4]  = result.itod_secs;
                TOD_INFO[5]  = result.itod_hunds;
                TOD_INFO[6]  = result.itod_timezone;
                TOD_INFO[7]  = result.itod_tinterval;
                TOD_INFO[8]  = result.itod_day;
                TOD_INFO[9]  = result.itod_month;
                TOD_INFO[10] = result.itod_year;
            TOD_INFO[11] = result.itod_weekday;

            // Free the buffer.
            NetApiBufferFree(pintBuffer);

            return TOD_INFO;

        }

        #endregion

}    // End class GetNetRemoteTOD
```

## Sample Code:
```cs
class Class1
    {
        [STAThread]
        static void Main(string[] args)
        {

            string ServerName = @"\\test01";
            GetNetRemoteTOD gnrTOD = new GetNetRemoteTOD();                        
            int[] TOD_Info = new int [12];            

            try
            {
                TOD_Info = gnrTOD.xNetRemoteTOD( ServerName );

            }
            catch(Exception err)
            {
                //report error
                Console.WriteLine ("NetRemoteTOD from " + ServerName + " failed!\nError: " + err.Message );
                return;
            }

            Console.Write("\r\nDate/Time from {0} : {1}.{2}.{3}  {4}:{5}:{6} TZ = {7}\r\n",
                    ServerName, TOD_Info[8], TOD_Info[9],
                    TOD_Info[10], TOD_Info[2], TOD_Info[3],
                    TOD_Info[4], TOD_Info[6]);

        }

    }    // End Class1
```

## Alternative Managed API:
```cs
using System.DirectoryServices.ActiveDirectory;

    DomainControllerCollection controllers = Domain.GetCurrentDomain().DomainControllers;
    foreach (DomainController c in controllers)
        Console.WriteLine(c.CurrentTime);
```
