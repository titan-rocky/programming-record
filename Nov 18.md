### 1.
```c
#include "stdio.h"

char *f();
char a = 'a';

int main( int argc, char *argv[] ){
    char* temp = f();
    printf("%s",temp);
    return 0;
}

char *f(){
    return &a;
}
```

#### Output
```
a
```
#### Explanation
- The `%s` accepts a string, which is actually a character pointer.
- But the temp points to a single character, and strings need a `\0` character to terminate. since this is a single character, this may result in a segfault.

### 2.
```c
#include "stdio.h"
#include "stdlib.h"

int main( int argc, char *argv[] ){
    char temp[20];
    gcvt(23.45,2,temp);
    printf("%s",temp);
    return 0;
}
```

#### Output
```
23
```
#### Explanation
`gcvt` function converts floating point to strings. 2 is the no of significant digits. The string will be stored in temp. 

### 3.
```c
#include "stdio.h"
#include "stdlib.h"

int main( int argc, char *argv[] ){
    int a = atoi("100");
    printf("%d",a);
    return 0;
}
```

#### Output
```
100
```
#### Explanation
`stdlib::atoi()` is a C function which converts a string which has a integer value,  in ASCII to the integer value mentioned in the string.

### 4.
```c
#include "stdio.h"

int main() {
    if (printf("cppbuzz")){
        printf("cppbuzz");
    }
    return 0;
}
```

#### Output
```
cppbuzzcppbuzz
```
Times=2
#### Explanation
- `printf` gets executed and returns the number of characters written in stdout.
- `printf("cppbuzz")` gets executed first in the if statement, printing a cppbuzz
- it returns 7, a truth value and thus the if statement gets executed
### 5.
```c
#include "stdio.h"

int main() {
    int x = 10;
    {
        int x=0;
        printf("%d",x);
    }
}
```

#### Output
```
0
```
#### Explanation
- the blocks without a statement will get executed without any errors locally
- the variables in block however have local scope and thus 0 is printed instead of 10

### 6.
```c
#include "stdio.h"

int main() {
    char *ptr1, *ptr2;
    printf("%d %d", sizeof(ptr1), sizeof(ptr2));
    return 0;
}
```

#### Output (32 Bit system)
```
4 4
```
#### Output (64 Bit system)
```
8 8
```
#### Explanation
- sizeof will return the number of bytes allocated for the variable.
- sizeof of a pointer will return the size of the pointer address

### 7.
```c
#include "stdio.h"

int a=20;

int main() {
    int a=10;
    printf("%d",a);
    return 0;
}
```

#### Output
```
10
```
#### Explanation
- `printf` lies in the main() scope and thus searches for the variable `x` in nearest scope i.e. local. Hence it returns 10

### 8.
```c
#include "stdio.h"

char *f();
char a = 'a';

int main() {
    char *temp = f();
    printf("%&",temp);
    return 0;
}

char *f() {
    return &a;
}
```

#### Output
```
%&
```
#### Explanation
- `%&` is not a valid conversion specifier in gcc
- Hence it prints it as a string of normal characters, with a warning.

### 9.
```c
#include "stdio.h"

int a=20;

int main() {
    int a=10;
    printf("%d",::a);
    return 0;
}
```

#### Output (g++)
```
20
```
#### Explanation
:: accesses the global scope

### 10.
```c
#include "stdio.h"

int main() {
    if (printf("C Programming is ")){
        printf("easy");
    } else {
        printf("hard");
    }
    return 0;
}
```

#### Output
```
C Programming is easy
```
#### Explanation
`printf()` returns the length of string since its been written in stdout. since the length is not zero, the if statement gets executed and thus 