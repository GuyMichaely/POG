# POG
Me publishing my responses to the Practice of Programming by K&amp;R

##Exercise 1-1
*Comment on the choice of names and values in the following code*
```? #define TRUE 0
? #define FALSE 1
?
? if ((ch = getchar()) == EOF)
? not-eof = FALSE;
```
**Comments:** 
Markup : * C uses non 0 values as true and 0 values as false, rather than the reverse as shown in the code. Hence, the two macro values should be swapped.
  * There doesn't appear to be a good reason to put (ch = getchar()) inside the if condition rather than setting it outside the if and comparing inside.
  * Line 5 does not do what it appears its programmer intended it to do. It sets `not-eof` to `FALSE`, which has the value 1, and 1 is truthy.
  * `not-eof` is an unnecesarily complicated name. Line 5 should be changed to `isEOF = TRUE` (once `TRUE` is appropriately changed) unless the programmer wishes to squeeze every last bit (pun intended) of performance from their code and comparing to false is more efficient.
