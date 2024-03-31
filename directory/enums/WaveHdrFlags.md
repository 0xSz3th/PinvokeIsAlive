
## C# Definition:
```cs
[Flags]
enum WaveHdrFlags : uint
{
   WHDR_DONE = 1,
   WHDR_PREPARED = 2,
   WHDR_BEGINLOOP = 4,
   WHDR_ENDLOOP = 8,
   WHDR_INQUEUE = 16 
}
```

## VB Definition:
```cs
<Flags()> _
Enum WaveHdrFlags As UInteger
  WHDR_DONE = 1
  WHDR_PREPARED = 2
  WHDR_BEGINLOOP = 4
  WHDR_ENDLOOP = 8
  WHDR_INQUEUE = 16
End Enum
```
