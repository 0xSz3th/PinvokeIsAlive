
## Sample Code:
```cs
public int nLength; //Useless field = 0
  public IntPtr pSecurityDescriptor; //хз))
  public bool bInheritHandle; //Возможность наследования

  public SecurityAttributes ()
  {
     this.bInheritHandle = true;
     this.nLength = 0;
     this.pSecurityDescriptor = IntPtr.Zero;
  }
}
```

## Sample Code:
```cs
bool Is;
  IntPtr Job = CreateJobObject (null, "Хуй =)");
  AssignProcessToJobObject(Job, GetCurrentProcess());

  IsProcessInJob (GetCurrentProcess (), Job, out Is);
  Console.WriteLine ("That process in that job: " + Is);

  IsProcessInJob (GetCurrentProcess (), IntPtr.Zero, out Is);
  Console.WriteLine ("That process in any job: " + Is);

  CloseHandle (Job);
  Console.ReadKey();
```
