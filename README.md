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
## Exercise 1-5
*What is wrong with this excerpt:*
```
? int read(int *ip) {
?   scanf ("%d", ip);
?   return *ip;
? }
? ...
? insert(&graph[vert] , read(&val) , read(&ch));
```

**Response:**

 * `read` has side effects via `scanf` and parameter evaluation order is undefined in C. Hence, calling
 `read` twice as function parameters to `insert` can undesireably swap the order of the values of the parameters of `insert`
 * `ch`'s type is implied to be `char`, meaning that `&char` is a `char*` whereas `read` requires a `int*`

## Exercise 1-6
*List all the different outputs this could produce with various orders of evaluation:*
```
? n = 1;
? printf("%d %d\n", n++, n++);
```

**Response:**

All conceivable combinations, because parameter evaluation and side effect orders are both undefined.
 * 1 1
 * 1 2
 * 1 3
 * 2 1
 * 2 2
 * 2 3
 * 3 1
 * 3 2
 * 3 3

## Exercise 1-7
*Rewrite these C/C++ excerpts more clearly:*

**Excerpt:**

```
? if (istty(stdin)) ;
?   else if (istty(stdout))) ;
?     else if (istty(stderr)) ;
?       else return(0);
```

**Rewritten:**

```
if (!istty(stdin) && !istty(stdout) && !istty(stderr)) {
  return 0;
}
```

Or, perhaps:

```
FILE *pipes[] = {stdin, stdout, stderr};
int haveTTY = 0;
for (int i = 0; i < 3; i++) {
  haveTTY = haveTTY || istty(pipes[i]);
}
if (haveTTY == 0) {
  return 0;
}
```

**Excerpt:**

```
? if (retval != SUCCESS) 
?   return (retval);
? }
? /* All went well! */
? return SUCCESS;
```

**Rewritten:**

```
return retval;
```

**Excerpt:**

```
? for (k = 0; k++ < 5; x += dx)
?   scanf("%lf", &dx);
```

**Rewritten:**

```
for (k = 0; k < 5; k++) {
  scanf("%lf", &dx);
  x += dx;
}
```

## Exercise 1-8
*Identify the errors in this Java fragment and repair it by rewriting with an idiomatic loop:*

**Excerpt:**

```
? int count = 0;
? while (count < total) {
?   count++;
?   if (this.getName(count) == nametable.userName()) {
?     return (true);
?   }
? }
```

**Rewritten:**

The error is that we increment count at the beginning of the loop, rather than the end.
```
for (int i = 0; i < total; i++) {
  if (this.getName(i) == nametable.userName()) {
    return true;
  }
}
```
