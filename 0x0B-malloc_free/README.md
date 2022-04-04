The malloc function is used to allocate a certain amount of memory during the execution of a program. It will request a block of memory from the heap. If the request is granted, the operating system will reserve the requested amount of memory and malloc will return a pointer to the reserved space.



When the amount of memory is not needed anymore, you must return it to the operating system by calling the function free.



Automatic allocation

When you declare variables or when you use strings within double quotes, the program is taking care of all the memory allocation. You do not have to think about it.



julien@ubuntu:~/c/malloc$ head -n 14 cisfun.c

/**

 * cisfun - function used for concept introduction

 * @n1: number of projects

 * @n2: number of tasks

 *

 * Return: nothing.

 */

void cisfun(unsigned int n1, unsigned int n2)

{

    int n;

    char c;

    int *ptr;

    char array[3];

}

julien@ubuntu:~/c/malloc$ 

In the above example, the arguments and the local variables are stored automatically in memory when the function is called. The program reserves space and uses it without you having to think about it.







By default, the memory used to store those variables can be read and written. When the program leaves the function, the memory used for all the above variables is released for future use.



Special case: string literals



One special case we have seen so far is the memory used to store strings that we put within double quotes (") in our programs. For instance:



char *str;



str = “Holberton”;

The string "Holberton" that was just declared is stored automatically in memory when the program is launched. But, the memory that stores the string is only readable. In fact, if you try to change a character using str, you will have a little surprise :)



julien@ubuntu:~/c/malloc$ cat segf.c

/**

 * segf - Let's segfault \o/

 *

 * Return: nothing.

 */

void segf(void)

{

    char *str;



    str = "Holberton";

    str[0] = 's';

}



/**

 *  main - concept introduction

 *

 * Return: 0.

 */

int main(void)

{

    segf();

    return (0);

}

julien@ubuntu:~/c/malloc$ gcc segf.c

julien@ubuntu:~/c/malloc$ ./a.out

Segmentation fault (core dumped)

julien@ubuntu:~/c/malloc$

In the above example, the variable str is a pointer to a char, that is initialized to the address of the first character of the string “Holberton”. But the memory storing the string “Holberton” is read-only, and will also not be released when the function returns. This is the state of the memory after the line str = "Holberton"; is executed (in red: read-only memory):
