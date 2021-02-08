# The Practice of Programming
Me publishing my responses to the Practice of Programming by K&amp;R

## Exercise 1-1
*Comment on the choice of names and values in the following code:*
```? #define TRUE 0
? #define FALSE 1
?
? if ((ch = getchar()) == EOF)
? not-eof = FALSE;
```
**Comments:** 
 * C uses non 0 values as true and 0 values as false, rather than the reverse as shown in the code. Hence, the two macro values should be swapped.
 * There doesn't appear to be a good reason to put (ch = getchar()) inside the if condition rather than setting it outside the if and comparing inside.
 * Line 5 does not do what it appears its programmer intended it to do. It sets `not-eof` to `FALSE`, which has the value 1, and 1 is truthy.
 * `not-eof` is an unnecesarily complicated name. Line 5 should be changed to `isEOF = TRUE` (once `TRUE` is appropriately changed) unless the programmer wishes to squeeze every last bit (pun intended) of performance from their code and comparing to false is more efficient.
## Exercise 1-2
*Improve this function:*
```
? int smaller(char *s, char *t) {
?   if (strcmp(s, t) < 1)
?     return 1;
?   else
?     return 0;
? }
```
**Response:** 

```
bool isSmaller(char *s, char *t) {
  return strcmp(s, t) < 0;
}
```
**Comments:**
 * No need to return an int if you're returning a boolean value
 * `return strcmp(s, t) < 0` is as clear as what it replaced and is more concise
 * The question code makes the comparison `strcmp(s, t) < 1`, yet the function is named *smaller*. When `strcmp(s, t) == 0`, `s` is not smaller than `t` yet `strcmp(s, t) < 1` is true. The code does not do what its name indicates

## Exercise 1-3
*Read this code aloud:*
```
? if ((falloc(SMRHSHSCRTCH, SJFEXT10644, MAXRODDHSH)) < 0)
? ...
```
**Comments:**
 * Lol

## Exercise 1-4
*Improve each of these fragments:*

**Fragment:**
```
? if ( !(c == 'y' || c == 'Y') )
?   return;
```
**Improved:**
```
if (c != 'y' && c != 'Y')
  return;
```
**Fragment:**
```
? length = (length < BUFSIZE) ? length: BUFSIZE;
```
**Improved:**
```
int min(int a, int b) {
  return a < b ? a : b;
}

length = min(length, BUFSIZE);
```
**Fragment:**
```
? flag = flag ? 0 : 1;
```
**Improved:**
```
flag = !flag;
```
**Fragment:**
```
? quote = (*line == '"') ? 1 : 0;
```
**Improved:**
```
isQuote = *line == '"';
```
**Fragment:**
```
? if (val & 1)
?   bit = 1;
? else
?   bit = 0;
```
**Improved:**
```
lastBit = val & 1;
```
