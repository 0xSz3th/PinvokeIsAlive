
## C# Signature:
```cs
[DllImport("psapi.dll", SetLastError = true)]
static extern bool GetPerformanceInfo(out PERFORMANCE_INFORMATION pPerformanceInformation, uint cb);
```

## VB Signature:
```cs
Declare Function GetPerformanceInfo Lib "psapi.dll" (TODO) As Boolean
```

## User-Defined Types:
```cs
[StructLayout(LayoutKind.Sequential)]
    public struct PERFORMANCE_INFORMATION
    {
        uint cb;
        UIntPtr CommitTotal;
        UIntPtr CommitLimit;
        UIntPtr CommitPeak;
        UIntPtr PhysicalTotal;
        UIntPtr PhysicalAvailable;
        UIntPtr SystemCache;
        UIntPtr KernelTotal;
        UIntPtr KernelPaged;
        UIntPtr KernelNonpaged;
        UIntPtr PageSize;
        uint HandleCount;
        uint ProcessCount;
        uint ThreadCount;
    }

    // Alternate Version, Fields Documented   
    [StructLayout( LayoutKind.Sequential )]
    private struct PerformanceInformation
    {
        /// <summary>The size of this structure, in bytes.</summary>
        public uint cb;
        /// <summary>The number of pages currently committed by the system. Note that committing 
        /// pages (using VirtualAlloc with MEM_COMMIT) changes this value immediately; however, 
        /// the physical memory is not charged until the pages are accessed.</summary>
        public UIntPtr  CommitTotal;
        /// <summary>The current maximum number of pages that can be committed by the system 
        /// without extending the paging file(s). This number can change if memory is added 
        /// or deleted, or if pagefiles have grown, shrunk, or been added. If the paging 
        /// file can be extended, this is a soft limit.</summary>
        public UIntPtr CommitLimit;
        /// <summary>The maximum number of pages that were simultaneously in the committed state 
        /// since the last system reboot.</summary>
        public UIntPtr CommitPeak;
        /// <summary>The amount of actual physical memory, in pages.</summary>
        public UIntPtr PhysicalTotal;
        /// <summary>The amount of physical memory currently available, in pages. This is the 
        /// amount of physical memory that can be immediately reused without having to write 
        /// its contents to disk first. It is the sum of the size of the standby, free, and 
        /// zero lists.</summary>
        public UIntPtr PhysicalAvailable;
        /// <summary>The amount of system cache memory, in pages. This is the size of the 
        /// standby list plus the system working set.</summary>
        public UIntPtr SystemCache;
        /// <summary>The sum of the memory currently in the paged and nonpaged kernel pools, in pages.</summary>
        public UIntPtr KernelTotal;
        /// <summary>The memory currently in the paged kernel pool, in pages.</summary>
        public UIntPtr KernelPaged;
        /// <summary>The memory currently in the nonpaged kernel pool, in pages.</summary>
        public UIntPtr KernelNonpaged;
        /// <summary>The size of a page, in bytes.</summary>
        public UIntPtr PageSize;
        /// <summary>The current number of open handles.</summary>
        public uint HandleCount;
        /// <summary>The current number of processes.</summary>
        public uint ProcessCount;
        /// <summary>The current number of threads.</summary>
        public uint ThreadCount;
    }
```

## Sample Code:
```cs
public class PerfomanceInfoData
  {
      public Int64 CommitTotalPages;
      public Int64 CommitLimitPages;
      public Int64 CommitPeakPages;
      public Int64 PhysicalTotalBytes;
      public Int64 PhysicalAvailableBytes;
      public Int64 SystemCacheBytes;
      public Int64 KernelTotalBytes;
      public Int64 KernelPagedBytes;
      public Int64 KernelNonPagedBytes;
      public Int64 PageSizeBytes;
      public int HandlesCount;
      public int ProcessCount;
      public int ThreadCount;
  }

  public static class PsApiWrapper
  {
    [DllImport("psapi.dll", SetLastError = true)]
    [return: MarshalAs(UnmanagedType.Bool)]
    private static extern bool GetPerformanceInfo([Out] out PsApiPerformanceInformation PerformanceInformation, [In] int Size);

    [StructLayout(LayoutKind.Sequential)]
    public struct PsApiPerformanceInformation
    {
      public int Size;
      public IntPtr CommitTotal;
      public IntPtr CommitLimit;
      public IntPtr CommitPeak;
      public IntPtr PhysicalTotal;
      public IntPtr PhysicalAvailable;
      public IntPtr SystemCache;
      public IntPtr KernelTotal;
      public IntPtr KernelPaged;
      public IntPtr KernelNonPaged;
      public IntPtr PageSize;
      public int HandlesCount;
      public int ProcessCount;
      public int ThreadCount;
    }

    public static PerfomanceInfoData GetPerformanceInfo()
    {
      PerfomanceInfoData data = new PerfomanceInfoData();
      PsApiPerformanceInformation perfInfo = new PsApiPerformanceInformation();
      if (GetPerformanceInfo(out perfInfo, Marshal.SizeOf(perfInfo)))
      {
    /// data in pages
    data.CommitTotalPages = perfInfo.CommitTotal.ToInt64();
    data.CommitLimitPages = perfInfo.CommitLimit.ToInt64();
    data.CommitPeakPages = perfInfo.CommitPeak.ToInt64();

    /// data in bytes
    Int64 pageSize = perfInfo.PageSize.ToInt64();
    data.PhysicalTotalBytes = perfInfo.PhysicalTotal.ToInt64() * pageSize;
    data.PhysicalAvailableBytes = perfInfo.PhysicalAvailable.ToInt64() * pageSize;
    data.SystemCacheBytes = perfInfo.SystemCache.ToInt64() * pageSize;
    data.KernelTotalBytes = perfInfo.KernelTotal.ToInt64() * pageSize;
    data.KernelPagedBytes = perfInfo.KernelPaged.ToInt64() * pageSize;
    data.KernelNonPagedBytes = perfInfo.KernelNonPaged.ToInt64() * pageSize;
    data.PageSizeBytes = pageSize;

    /// counters
    data.HandlesCount = perfInfo.HandlesCount;
    data.ProcessCount = perfInfo.ProcessCount;
    data.ThreadCount = perfInfo.ThreadCount;
      }
      return data;
    }
  }
```

## Sample Code:
```cs
// Alternate Version, Method Wrapped So It Can Be Easily Replaced In The Future
    // While Minimizing Impact To Existing Code
    [return: MarshalAs( UnmanagedType.Bool )]
    [DllImport( "psapi.dll", CharSet = CharSet.Auto, EntryPoint = "GetPerformanceInfo", SetLastError = true )]
    static extern bool _GetPerformanceInfo( ref PerformanceInformation pi, uint cb );

    /// <summary>Wrapper for native GetPerformanceInfo function - returns performance values</summary>
    /// <param name="pi">Instance of <see cref="PerformanceInformation"/> structure to populate</param>
    /// <returns>True if the function call was successful, false otherwise.  Check <see cref="Marshal.GetLastWin32Error"/> 
    /// for additional information.</returns>
    public static bool GetPerformanceInfo( ref PerformanceInformation pi )
    {
        pi.cb = (uint)Marshal.SizeOf( pi.GetType() );

        var _ret = _GetPerformanceInfo( ref pi, pi.cb );

        return( _ret );
    }
```
