
## C# Signature:
```cs
[DllImport("icmp.dll", SetLastError=true)]
static extern Int32 IcmpSendEcho(IntPtr icmpHandle, Int32 destinationAddress, IntPtr requestData, Int16 requestSize, IntPtr requestOptions, IntPtr replyBuffer, Int32 replySize, Int32 timeout);
```

## VB Signature:
```cs
Declare Function IcmpSendEcho Lib "icmp.dll" (icmpHandle as IntPtr, destinationAddress as Int32, requestData as IntPtr, requestSize as Int16, requestOptions as IntPtr, replyBuffer as IntPtr, replySize as Int32, timeout as Int32) As Int32
```

## Sample Code:
```cs
using System;
    using System.Net;
    using System.Runtime.InteropServices;

    public class IcmpPing
    {
        [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
        private struct ICMP_OPTIONS
        {
            public byte Ttl;
            public byte Tos;
            public byte Flags;
            public byte OptionsSize;
            public IntPtr OptionsData;
        }

        [StructLayout(LayoutKind.Sequential, CharSet=CharSet.Ansi)]
        private struct ICMP_ECHO_REPLY
        {
            public int Address;
            public int Status;
            public int RoundTripTime;
            public short DataSize;
            public short Reserved;
            public IntPtr DataPtr;
            public ICMP_OPTIONS Options;
            [MarshalAs(UnmanagedType.ByValTStr, SizeConst=250)]
            public string Data;
        }

        [DllImport("icmp.dll", SetLastError=true)]
        private static extern IntPtr IcmpCreateFile();
        [DllImport("icmp.dll", SetLastError=true)]
        private static extern bool IcmpCloseHandle(IntPtr handle);
        [DllImport("icmp.dll", SetLastError=true)]
        private static extern int IcmpSendEcho(IntPtr icmpHandle, int destinationAddress, string requestData, short requestSize, ref ICMP_OPTIONS requestOptions, ref ICMP_ECHO_REPLY replyBuffer, int replySize, int timeout);

        public bool Ping(IPAddress ip)
        {
            IntPtr icmpHandle = IcmpCreateFile();
            ICMP_OPTIONS icmpOptions = new ICMP_OPTIONS();
            icmpOptions.Ttl = 255;
            ICMP_ECHO_REPLY icmpReply = new ICMP_ECHO_REPLY();
            string sData = "x";

            int iReplies = IcmpSendEcho(icmpHandle, BitConverter.ToInt32(ip.GetAddressBytes(), 0), sData, (short)sData.Length, ref icmpOptions, ref icmpReply, Marshal.SizeOf(icmpReply), 30);
            IcmpCloseHandle(icmpHandle);
            if (icmpReply.Status == 0)
                return true;
            return false;
        }
    }
```

## Sample Code:
```cs
tcc -Wall ping.c /WINDOWS/system32/iphlpapi.dll /windows/system32/ws2_32.dll
```

## Sample Code:
```cs
gcc -Wall -Wl,--enable-stdcall-fixup ping.c -liphlpapi

// still not quite sure what the times are, e.g., the max time can be set at
// 5 mSec and we successfully complete the ping in 188 mSec... should timeout.

#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <time.h>
#include <windows.h>

#ifdef __CYGWIN__
#include <cygwin/in.h>
#include <w32api/ipexport.h>
#include <w32api/icmpapi.h>
#include <arpa/inet.h>
#endif

// for tinyc, pull definitions out of cygwin /usr/include/w32api/...
#ifdef __TINYC__
// _ming.h:
#ifndef __LP64__    /* 32 bit target, 64 bit Mingw target */
#define __LONG32 long
#else            /* 64 bit Cygwin target */
#define __LONG32 int
#endif

// winsock.h:
#define INADDR_NONE 0xffffffff
#ifndef WINSOCK_API_LINKAGE
#ifdef  DECLSPEC_IMPORT
#define WINSOCK_API_LINKAGE    DECLSPEC_IMPORT
#else
#define WINSOCK_API_LINKAGE
#endif
#endif /* WINSOCK_API_LINKAGE */
#define WSAAPI            WINAPI
WINSOCK_API_LINKAGE unsigned __LONG32 WSAAPI inet_addr(const char *cp);

// ipexport.h:
typedef ULONG IPAddr;
typedef ULONG IPMask;

typedef struct ip_option_information {
   UCHAR Ttl;
   UCHAR Tos;
   UCHAR Flags;
   UCHAR OptionsSize;
   PUCHAR OptionsData;
} IP_OPTION_INFORMATION,*PIP_OPTION_INFORMATION;

typedef struct icmp_echo_reply {
   IPAddr Address;
   ULONG Status;
   ULONG RoundTripTime;
   USHORT DataSize;
   USHORT Reserved;
   PVOID Data;
   struct ip_option_information Options;
} ICMP_ECHO_REPLY,*PICMP_ECHO_REPLY;

// /usr/include/w32api/icmpapi.h
HANDLE WINAPI IcmpCreateFile(VOID);
WINBOOL WINAPI IcmpCloseHandle(HANDLE IcmpHandle);
DWORD WINAPI IcmpSendEcho(HANDLE IcmpHandle, IPAddr DestinationAddress, 
    LPVOID RequestData, WORD RequestSize,
    PIP_OPTION_INFORMATION RequestOptions, LPVOID ReplyBuffer,
    DWORD ReplySize,DWORD Timeout);

#endif

int main(int argc, char **argv)  {

    int maxMsec = 100;

    // Declare and initialize variables

    unsigned long ipaddr = INADDR_NONE;
    DWORD dwRetVal = 0;
    char SendData[32] = "Data Buffer";
    LPVOID ReplyBuffer = NULL;
    DWORD ReplySize = 0;

    HANDLE hIcmpFile = IcmpCreateFile();
    if (hIcmpFile == INVALID_HANDLE_VALUE) {
        printf("IcmpCreatefile returned error: %ld\n", GetLastError());
        exit(1);
    }

    ReplySize = sizeof(ICMP_ECHO_REPLY) + sizeof(SendData);
    ReplyBuffer = (VOID*) malloc(ReplySize);
    if (ReplyBuffer == NULL) {
        printf("Unable to allocate ReplyBuffer memory\n");
        exit(1);
    }    

    // get numeric address
    char *ip_addr_str = strdup("149.20.53.86");     // www.netbsd.org: 
    if (INADDR_NONE == (ipaddr = inet_addr(ip_addr_str))) {
        printf("!inet_addr(\"%s\")\n", ip_addr_str);
        exit(1);
    }

    // do ping
    dwRetVal = IcmpSendEcho(hIcmpFile, ipaddr, SendData, sizeof(SendData), 
        NULL, ReplyBuffer, ReplySize, maxMsec);

    // != 0 can still be dest unreachable, test status further down too
    if (dwRetVal == 0) {
        printf("No reply from %s after %d mSec\n", ip_addr_str, maxMsec);
        return 1;
    }

    PICMP_ECHO_REPLY pEchoReply = (PICMP_ECHO_REPLY)ReplyBuffer;
    if (0 != pEchoReply->Status) {
        printf("no reply from %s after %d mSec\n", ip_addr_str, maxMsec);
        return 1;
    }

    printf("Roundtrip time to %s = %ld mSec\n", ip_addr_str,
        pEchoReply->RoundTripTime);

    IcmpCloseHandle(hIcmpFile);

    return 0;
}
```
