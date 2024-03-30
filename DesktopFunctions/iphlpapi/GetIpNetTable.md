
## C# Signature:
```cs
[DllImport("iphlpapi.dll", EntryPoint="GetIpNetTable")]
static extern int GetIpNetTable(IntPtr pIpNetTable, ref int pdwSize, bool bOrder);
```

## VB.NET Signature:
```cs
<DllImport("IpHlpApi.dll")>
    Private Shared Function GetIpNetTable(pIpNetTable As IntPtr, <MarshalAs(UnmanagedType.U4)> ByRef pdwSize As Integer, bOrder As Boolean) As <MarshalAs(UnmanagedType.U4)> Integer
    End Function
```

##  C# User-Defined Types:
```cs
// Define the MIB_IPNETROW structure.      
    [StructLayout(LayoutKind.Sequential)]     
    struct MIB_IPNETROW      
    {     
        [MarshalAs(UnmanagedType.U4)]     
        public uint dwIndex;     
        [MarshalAs(UnmanagedType.U4)]     
        public uint dwPhysAddrLen;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac0;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac1;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac2;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac3;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac4;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac5;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac6;     
        [MarshalAs(UnmanagedType.U1)]     
        public byte mac7;     
        [MarshalAs(UnmanagedType.U4)]     
        public uint dwAddr;     
        [MarshalAs(UnmanagedType.U4)]     
        public uint dwType;      
    }
```

##  VB.NET User-Defined Types:
```cs
Public Const ERROR_SUCCESS As Integer = 0
    Public Const ERROR_INSUFFICIENT_BUFFER As Integer = 122
```

##  VB.NET User-Defined Types:
```cs
<MarshalAs(UnmanagedType.U4)>
    Public dwIndex As UInteger
    <MarshalAs(UnmanagedType.U4)>
    Public dwPhysAddrLen As UInteger
    <MarshalAs(UnmanagedType.ByValArray, SizeConst:=6)>
    Public bPhysAddr() As Byte
    <MarshalAs(UnmanagedType.U4)>
    Public dwAddr As UInteger
    <MarshalAs(UnmanagedType.U4)>
    Public dwType As DWTYPES
```

##  VB.NET User-Defined Types:
```cs
<MarshalAs(UnmanagedType.U4)>
    Other = 1
    <MarshalAs(UnmanagedType.U4)>
    Invalid = 2
    <MarshalAs(UnmanagedType.U4)>
    Dynamic = 3
    <MarshalAs(UnmanagedType.U4)>
    [Static] = 4
```

## C# Sample Code:
```cs
//http://stackoverflow.com/questions/1148778/how-do-i-access-arp-protocol-information-through-c-net
    using System;
    using System.Runtime.InteropServices;
    using System.ComponentModel; 
    using System.Net;

    namespace GetIpNetTable
    {   
    class Program   {      
        // The max number of physical addresses.      
        const int MAXLEN_PHYSADDR = 8;      
          // Declare the GetIpNetTable function.
          [DllImport("IpHlpApi.dll")]
          [return: MarshalAs(UnmanagedType.U4)]
          static extern int GetIpNetTable(
         IntPtr pIpNetTable,
         [MarshalAs(UnmanagedType.U4)]
         ref int pdwSize,
         bool bOrder);
          // The insufficient buffer error.
          const int ERROR_INSUFFICIENT_BUFFER = 122;
          static void Main(string[] args)
          {
         // The number of bytes needed.
         int bytesNeeded = 0;
         // The result from the API call.
         int result = GetIpNetTable(IntPtr.Zero, ref bytesNeeded, false);
         // Call the function, expecting an insufficient buffer.
         if (result != ERROR_INSUFFICIENT_BUFFER)
         {
            // Throw an exception.
            throw new Win32Exception(result);
         }
         // Allocate the memory, do it in a try/finally block, to ensure
         // that it is released.
         IntPtr buffer = IntPtr.Zero; 

         // Try/finally.
         try
         {
            // Allocate the memory.
            buffer = Marshal.AllocCoTaskMem(bytesNeeded);
            // Make the call again. If it did not succeed, then
            // raise an error.
            result = GetIpNetTable(buffer, ref bytesNeeded, false);
            // If the result is not 0 (no error), then throw an exception.
            if (result != 0)
            {
               // Throw an exception.
               throw new Win32Exception(result);
            }
            // Now we have the buffer, we have to marshal it. We can read
            // the first 4 bytes to get the length of the buffer.
            int entries = Marshal.ReadInt32(buffer);
            // Increment the memory pointer by the size of the int.
            IntPtr currentBuffer = new IntPtr(buffer.ToInt64() +
               Marshal.SizeOf(typeof(int)));     

            // Allocate an array of entries.
            MIB_IPNETROW[] table = new MIB_IPNETROW[entries];
            // Cycle through the entries.
            for (int index = 0; index < entries; index++)
            {
               // Call PtrToStructure, getting the structure information.
               table[index] = (MIB_IPNETROW) Marshal.PtrToStructure(new
              IntPtr(currentBuffer.ToInt64() + (index *
              Marshal.SizeOf(typeof(MIB_IPNETROW)))), typeof(MIB_IPNETROW));
            }
            for (int index = 0; index < entries; index++)
            {
               IPAddress ip=new IPAddress(table[index].dwAddr);
               Console.Write("IP:"+ip.ToString()+"\t\tMAC:");
               byte b;
               b=table[index].mac0;
               if ( b < 0x10)
               {
              Console.Write("0");
               }
               else
               {
              Console.Write("");
               }
               Console.Write(b.ToString("X"));
               b=table[index].mac1;
               if ( b < 0x10)
               {
              Console.Write("-0");
               }
               else
               {
              Console.Write("-");
               }
               Console.Write(b.ToString("X"));
               b=table[index].mac2;
               if ( b < 0x10)
               {
              Console.Write("-0");
               }
               else
               {
              Console.Write("-");
               }
               Console.Write(b.ToString("X"));
               b=table[index].mac3;
               if ( b < 0x10)
               {
              Console.Write("-0");
               }
               else
               {
              Console.Write("-");
               }
               Console.Write(b.ToString("X"));
               b=table[index].mac4;
               if ( b < 0x10)
               {
              Console.Write("-0");
               }
               else
               {
              Console.Write("-"); 
               }
               Console.Write(b.ToString("X"));
               b=table[index].mac5;
               if ( b < 0x10)
               {
              Console.Write("-0");
               }
               else
               {
              Console.Write("-");
               }
               Console.Write(b.ToString("X"));
               Console.WriteLine();
            }
         }
         finally
         {
            // Release the memory.
            Marshal.FreeCoTaskMem(buffer);
         }
          }
       }
    }
```

## VB.NET Sample Code:
```cs
Public Shared Sub GetARPTablr()
    ' The number of bytes needed.
    Dim bytesNeeded As Integer = 0
    ' The result from the API call.
    Dim result As Integer = GetIpNetTable(IntPtr.Zero, bytesNeeded, False)
    ' Call the function, expecting an insufficient buffer.
    If result <> ERROR_INSUFFICIENT_BUFFER Then
        ' Throw an exception.
        Throw New Win32Exception(result)
    End If
    ' Allocate the memory, do it in a try/finally block, to ensure
    ' that it is released.
    Dim buffer As IntPtr = IntPtr.Zero

    ' Try/finally.
    Try
        ' Allocate the memory.
        buffer = Marshal.AllocCoTaskMem(bytesNeeded)
        ' Make the call again. If it did not succeed, then
        ' raise an error.
        result = GetIpNetTable(buffer, bytesNeeded, False)
        ' If the result is not 0 (no error), then throw an exception.
        If result <> ERROR_SUCCESS Then
        ' Throw an exception.
        Throw New Win32Exception(result)
        End If
        ' Now we have the buffer, we have to marshal it. We can read
        ' the first 4 bytes to get the length of the buffer.
        Dim entries As Integer = Marshal.ReadInt32(buffer)
        ' Increment the memory pointer by the size of the int.
        Dim currentBuffer As New IntPtr(buffer.ToInt64() + Marshal.SizeOf(GetType(Integer)))

        ' Allocate an array of entries.
        Dim table As MIB_IPNETROW() = New MIB_IPNETROW(entries - 1) {}
        ' Cycle through the entries.
        For index As Integer = 0 To entries - 1
        ' Call PtrToStructure, getting the structure information.
        table(index) = DirectCast(Marshal.PtrToStructure(New IntPtr(currentBuffer.ToInt64() + (index * Marshal.SizeOf(GetType(MIB_IPNETROW)))), GetType(MIB_IPNETROW)), MIB_IPNETROW)
        Next
        For index As Integer = 0 To entries - 1
        If table(index).dwType <> DWTYPES.Invalid And table(index).dwType <> DWTYPES.Other Then
            Dim ip As New IPAddress(table(index).dwAddr)
            Dim mac As New PhysicalAddress(table(index).bPhysAddr)

            Console.WriteLine(table(index).dwType.ToString & vbTab & vbTab & "IP:" + ip.ToString() & vbTab & vbTab & "MAC: " & MACtoString(mac))
        End If
        Next
    Finally
        ' Release the memory.
        Marshal.FreeCoTaskMem(buffer)
        '  Marshal.FreeHGlobal(rowptr)
    End Try
    End Sub

    Public Shared Function MACtoString(mac As PhysicalAddress, Optional Capital As Boolean = True) As String
    If Capital Then ' In capital Letters
        Return String.Join(":", (From z As Byte In mac.GetAddressBytes Select z.ToString("X2")).ToArray())
    Else
        Return String.Join(":", (From z As Byte In mac.GetAddressBytes Select z.ToString("x2")).ToArray())
    End If
    End Function
```
