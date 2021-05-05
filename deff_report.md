# Code Modification Report

## user.h
baris 29-31:
```C
#ifdef CS333_P1
int date(struct rtcdate*);
#endif // CS333_P1
```

## usys.s
baris 33:
```
SYSCALL(date)
```

## syscall.h
baris 27:
```C
#define SYS_date    SYS_halt+1
```
## syscall.c
baris 141-143:
```C
#ifdef CS333_P1
[SYS_date]    sys_date,
#endif // CS333_P1
```
baris 186-188:
```C
#ifdef PRINT_SYSCALLS
        cprintf("%s -> %d\n", syscallnames[num], curproc->tf->eax);
    #endif // PRINT_SYSCALLS
```
## sysproc.c
baris 101-113:
```C
#ifdef CS333_P1
int
sys_date(void)
{
  struct rtcdate *d;

  if(argptr(0, (void*)&d, sizeof(struct rtcdate)) < 0){
    return -1;
  }
    cmostime(d);
    return 0;
}

#endif // CS333_P1
```

## proc.h
baris 52:
```C
uint start_ticks;
```

## proc.c
baris 151:
```C
p->start_ticks = ticks;

```
baris 562-574:
```C
#elif defined(CS333_P1)
void
procdumpP1(struct proc *p, char *state_string)
{
  #ifdef C5333_P1
  int eim = ticks - p->start_ticks;
  int es = eim/ 1000;
  int me = eim % 1000;
  cprintf("%d\t%s\t%d.%d\t%s\t%d\t", p->pid, p->name, es, me, state_string, p->sz);
  #endif// C5333_P1
  return;
}
#endif
```

