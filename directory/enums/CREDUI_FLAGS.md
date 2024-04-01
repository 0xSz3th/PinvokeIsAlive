# CREDUI\_FLAGS

///

&#x20;   /// http://msdn.microsoft.com/library/default.asp?url=/library/en-us/dnnetsec/html/dpapiusercredentials.asp     /// http://msdn.microsoft.com/library/default.asp?url=/library/en-us/secauthn/security/creduipromptforcredentials.asp     ///    \[Flags]     public enum PromptForWindowsCredentialsFlags     {     ///    /// The caller is requesting that the credential provider return the user name and password in plain text.     /// This value cannot be combined with SECURE\_PROMPT.     ///    CREDUIWIN\_GENERIC = 0x1,     ///    /// The Save check box is displayed in the dialog box.     ///    CREDUIWIN\_CHECKBOX = 0x2,

&#x20;   REQUEST\_ADMINISTRATOR = 0x4,     EXCLUDE\_CERTIFICATES = 0x8,

&#x20;   ///

&#x20;   /// Only credential providers that support the authentication package specified by the authPackage parameter should be enumerated.     /// This value cannot be combined with CREDUIWIN\_IN\_CRED\_ONLY.     ///    CREDUIWIN\_AUTHPACKAGE\_ONLY = 0x10,     ///    /// Only the credentials specified by the InAuthBuffer parameter for the authentication package specified by the authPackage parameter should be enumerated.     /// If this flag is set, and the InAuthBuffer parameter is NULL, the function fails.     /// This value cannot be combined with CREDUIWIN\_AUTHPACKAGE\_ONLY.     ///    CREDUIWIN\_IN\_CRED\_ONLY = 0x20,

&#x20;   SHOW\_SAVE\_CHECK\_BOX = 0x40,     ALWAYS\_SHOW\_UI = 0x80,

&#x20;   ///

&#x20;   /// Credential providers should enumerate only administrators. This value is intended for User Account Control (UAC) purposes only. We recommend that external callers not set this flag.     ///    CREDUIWIN\_ENUMERATE\_ADMINS = 0x100,     ///    /// Only the incoming credentials for the authentication package specified by the authPackage parameter should be enumerated.     ///    CREDUIWIN\_ENUMERATE\_CURRENT\_USER = 0x200,

&#x20;   VALIDATE\_USERNAME = 0x400,     COMPLETE\_USERNAME = 0x800,

&#x20;   ///

&#x20;   /// The credential dialog box should be displayed on the secure desktop. This value cannot be combined with CREDUIWIN\_GENERIC.     /// Windows Vista: This value is not supported until Windows Vista with SP1.     ///    CREDUIWIN\_SECURE\_PROMPT = 0x1000,

&#x20;   SERVER\_CREDENTIAL = 0x4000,     EXPECT\_CONFIRMATION = 0x20000,     GENERIC\_CREDENTIALS = 0x40000,     USERNAME\_TARGET\_CREDENTIALS = 0x80000,

&#x20;   ///

&#x20;   /// The credential provider should align the credential BLOB pointed to by the refOutAuthBuffer parameter to a 32-bit boundary, even if the provider is running on a 64-bit system.     ///    CREDUIWIN\_PACK\_32\_WOW = 0x10000000,     }
