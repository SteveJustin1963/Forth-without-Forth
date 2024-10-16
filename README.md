# Forth-without-Forth
- copy of repo info


[facebook](https://www.facebook.com/groups/1304548976637542/user/1329679734/?__cft__[0]=AZWrAULUN8cVzo8AauXzaIgieigiRECS9Rg6VPZ91KjveDp01-ltPskW69vxlzadvp3z5SIpfrp9eSNlUTBdRIE3l87RVGWkvfRoyYWoJj-OWetypnMrFQQEZ9RExLCpoA5kgxiuMear-CxAIjlJjS6lP7-nYMhTBzbsWs0WJMM43HRCEQTIBt4APnWKcMiSLEU&__tn__=-UC%2CP-R)      

### Chochain Lee

```
" Most Forths manage their memory carefully and manually with fixed blocks.
On the other end of spectrum, C++ has a vector class which manages its size (and allocation) 'magically'.
While collaborating with Dr. Ting in 2021 on his Forth without Forth paradigm,
we tried using vector for stacks, dictionary and parameter memory.
After a recent revision, I now have a full-fledged eForth that does not keep HERE,
have no S, R, or even IP which kind-of breaks the traditional wisdom of Forth.
Everything in one file, 359 lines.
See https://chochain.github.io/eforth/orig/ting/ceForth_410.cpp
and the inner interpreter in snip below.
The question is, unlike on MCU or FPGA, does manage your small blocks of memories
on top of Windows or Linux/iOS memory system making sense? Is it more efficient?
To my surprise, the vector-based token-threaded implementation out pace my classic
linear-memory subroutine-threaded by 10%.
Owch!
It means C++ compiler optimizer does better than my hand crafting one.
For my ego, I got to fix that! "
```

### code
- https://chochain.github.io/eforth/orig/ting/ceForth_410.cpp?

