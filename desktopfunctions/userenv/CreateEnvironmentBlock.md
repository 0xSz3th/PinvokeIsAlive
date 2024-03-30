
## C# Signature:
```cs
[DllImport("userenv.dll", SetLastError=true)]
static extern bool CreateEnvironmentBlock( out IntPtr lpEnvironment, IntPtr hToken, bool bInherit );
```

## VB Signature:
```cs
<DllImport("userenv.dll")> _
    Public Shared Function CreateEnvironmentBlock(ByRef lpEnvironment As IntPtr, ByVal hToken As IntPtr, ByVal bInherit As Boolean) As Boolean
    End Function
```

## Sample Code:
```cs
[DllImport("userenv.dll", SetLastError = true)]
        internal static extern bool CreateEnvironmentBlock(ref IntPtr lpEnvironment, IntPtr hToken, bool bInherit);
        /// <summary>
        /// Create an environment
        /// </summary>
        /// <param name="token">The security token</param>
        /// <param name="inherit">Inherit the environment from the calling process</param>
        /// <returns>a dictionary that represents the environ</returns>
        internal static Dictionary<string,string> CreateEnvironmentBlock(SecurityToken token, bool inherit) {
        IntPtr env = IntPtr.Zero;
        if (!CreateEnvironmentBlock(ref env, token, inherit)) {
            int lastError = Marshal.GetLastWin32Error();
            throw new System.ComponentModel.Win32Exception(lastError, "CreateEnvironmentBlock Error " + lastError);
        }
        Dictionary<String, String> userEnvironment = new Dictionary<string, string>();
        try {
            StringBuilder testData = new StringBuilder("");
            unsafe {
            short* start = (short*)env.ToPointer();
            bool done = false;
            short* current = start;
            while (!done) {
                if ((testData.Length > 0) && (*current == 0) && (current != start)) {
                String data = testData.ToString();
                int index = data.IndexOf('=');
                if (index == -1) {
                    userEnvironment.Add(data, "");
                } else if (index == (data.Length - 1)) {
                    userEnvironment.Add(data.Substring(0, index), "");
                } else {
                    userEnvironment.Add(data.Substring(0, index), data.Substring(index + 1));
                }
                testData.Length = 0;
                }
                if ((*current == 0) && (current != start) && (*(current - 1) == 0)) {
                done = true;
                }
                if (*current != 0) {
                testData.Append((char)*current);
                }
                current++;
            }
            }
        } finally {
            DestroyEnvironmentBlock(env);
        }
        return userEnvironment;
        }
    /// <summary>
    /// Create a byte array that represents the environment for 
    /// the different CreateProcess calls
    /// </summary>
    /// <param name="env">The input environment</param>
    /// <returns>A byte array</returns>
    private byte[] CreateEnvironment(Dictionary<string, string> env) {
        MemoryStream ms = new MemoryStream();
        StreamWriter w = new StreamWriter(ms, Encoding.Unicode);
        w.Flush();
        ms.Position = 0; //Skip any byte order marks to identify the encoding
        Char nullChar = (char)0;
        foreach (string k in env.Keys) {
        w.Write("{0}={1}", k, env[k]);
        w.Write(nullChar);
        }
        w.Write(nullChar);
        w.Write(nullChar);
        w.Flush();
        ms.Flush();
        byte[] data = ms.ToArray();
        return data;
    }
```
