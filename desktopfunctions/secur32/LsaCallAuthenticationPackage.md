
## C# Signature:
```cs
/// <summary>
    /// http://msdn2.microsoft.com/en-us/library/aa378261.aspx
    /// </summary>
    /// <param name="LsaHandle">[in] Handle obtained from a previous call to LsaRegisterLogonProcess or LsaConnectUntrusted.</param>
    /// <param name="AuthenticationPackage">[in] Supplies the identifier of the authentication package. This value is obtained by calling LsaLookupAuthenticationPackage.</param>
    /// <param name="ProtocolSubmitBuffer">[in] An authentication package–specific message buffer passed to the authentication package.</param>
    /// <param name="SubmitBufferLength">[in] Indicates the length of the ProtocolSubmitBuffer buffer, in bytes.</param>
    /// <param name="ProtocolReturnBuffer">[out] Pointer that receives the address of the buffer returned by the authentication package.</param>
    /// <param name="ReturnBufferLength">[out] Pointer to a ULONG that receives the length of the returned buffer, in bytes.</param>
    /// <param name="ProtocolStatus">[out] If the function succeeds, this parameter receives a pointer to an NSTATUS code which indicates the completion status of the authentication package.</param>
    /// <returns>If the function succeeds, the return value is STATUS_SUCCESS. Check the ProtocolStatus parameter to obtain the status returned by the authentication package.
    /// If the function fails, the return value is an NTSTATUS code. The following are possible error codes.
    ///     STATUS_QUOTA_EXCEEDED   The call could not be completed because the client's memory quota is not sufficient to allocate the return buffer. 
    ///     STATUS_NO_SUCH_PACKAGE  The specified authentication package is not recognized by the LSA. 
    /// </returns>
    [DllImport("Secur32.dll", SetLastError = true)]
    internal static extern int LsaCallAuthenticationPackage(
        [In] IntPtr LsaHandle,
        [In] IntPtr AuthenticationPackage,
        [In] IntPtr ProtocolSubmitBuffer,
        [In] UInt32 SubmitBufferLength,
        [Out] IntPtr ProtocolReturnBuffer,
        [Out] ref UInt32 ReturnBufferLength,
        [Out] int ProtocolStatus
        );
```

## VB Signature:
```cs
Declare Function LsaCallAuthenticationPackage Lib "secur32.dll" (TODO) As TODO
```
