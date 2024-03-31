
## C# Definition:
```cs
delegate CopyProgressResult CopyProgressRoutine(
    long TotalFileSize,
    long TotalBytesTransferred,
    long StreamSize,
    long StreamBytesTransferred,
    uint dwStreamNumber,
    CopyProgressCallbackReason dwCallbackReason,
    IntPtr hSourceFile,
    IntPtr hDestinationFile,
    IntPtr lpData);
```
