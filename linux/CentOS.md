# CentOS commands

with `grep` there are a few ways to find one of a given amount of words.  
Dont use `egrep`, its depricated and is only here to let historical applications rely on it to run unmodified.

Just use or operator |, remember to escape it:

 ```
 grep -i 'STRING1\|STRING2'
 ```
 
Or using grep with -E option:
 ```
grep -iE 'STRING1|STRING2'
 ```
 
Or -e:

 ```
grep -i -e 'STRING' -e 'STRING2'
 ```
 
 
