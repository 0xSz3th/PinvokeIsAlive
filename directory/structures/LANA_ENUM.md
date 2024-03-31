
## C# Definition:
```cs
struct LANA_ENUM {
   public TODO;
}
```

## VB Definition:
```cs
Private Const NCBENUM As Integer = &H37
Private Const MAX_LANA As Integer = 254

<StructLayout(LayoutKind.Sequential)> _
Private Structure LANA_ENUM
   Dim length As Byte
   <MarshalAs(UnmanagedType.ByValArray, SizeConst:=MAX_LANA + 1)> Dim lana() As Byte
End Structure
```

## Notes:
```cs
/*
  *  Structure returned to the NCB command NCBENUM.
  *
  *  On a system containing lana's 0, 2 and 3, a structure with
  *  length =3, lana[0]=0, lana[1]=2 and lana[2]=3 will be returned.
  */

typedef struct _LANA_ENUM {
   UCHAR   length;     //  Number of valid entries in lana[]
   UCHAR   lana[MAX_LANA+1];
} LANA_ENUM, *PLANA_ENUM;
```
