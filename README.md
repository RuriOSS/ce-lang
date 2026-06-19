# WIP:
Nothoing implemented yet, just some design ideas.
# About CE-lang:
Just a cute error handling extension for C, with no syntax breaking, and the tail will never wag the cat.
We will have a happy face `:>` for default handling, and a sad face `:<` for error handling.
# Why CE-lang:
In ruri:      
```c
res = seccomp_rule_add(ctx, SCMP_ACT_ALLOW, SCMP_SYS(bind), 0);
ruri_check_seccomp_ret(res, container->no_warnings);
```
Too ugly you see.     
seccomp_rule_add() uses va_args, so if you don't use these complex code, you can only use a macro. But in cross-arch ci, it will bomb to TLE, as the performance of macro is not good, and qemu is slow.      
So, I want a:     
```ce
seccomp_rule_add(ctx, SCMP_ACT_ALLOW, SCMP_SYS(bind), 0) :<;
```
It's better, right?    
And it will be auto expanded to:    
```c
if(seccomp_rule_add(ctx, SCMP_ACT_ALLOW, SCMP_SYS(bind), 0) != 0) {
    warning("seccomp_rule_add", __FILE__, __LINE__, res, errno);
}
```
So that's CE lang, C with better Error handling/Cute Error handling.    
The tail will never wag the cat.    
So ce-lang will never break c syntax, except the old `:>` as `]` design. But as ce will translate .ce to c, and if you only use `:>` as happy face in .ce, that's fine.    
So we have a very kawaii error handling in C now.    