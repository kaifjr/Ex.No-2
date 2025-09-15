# Ex.No :2
# GENERATION OF LEXICAL TOKENS USING LEX/FLEX TOOL
## Register Number : 212222043004
## Date : 09/09/2025
## AIM
 To write a lex program to implement lexical analyzer to recognize a few patterns.
## ALGORITHM

1.	Start the program.

2.	Lex program consists of three parts.

     a.	Declaration %%

     b.	Translation rules %%

     c.	Auxilary procedure.

3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form

    a.	P1 {action}

    b.	P2 {action}

    c.	…

    d.	…

    e.	Pn {action}

5.	Write a program in the vi editor and save it with .l extension.

6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.

## PROGRAM:
```

#include <stdio.h>
#include <ctype.h>
#include <string.h>

int isKeyword(char buffer[]) {
    char keywords[8][10] = {"if", "else", "while", "for", "int", "return", "char", "float"};
    for (int i = 0; i < 8; ++i) {
        if (strcmp(buffer, keywords[i]) == 0) {
            return 1;
        }
    }
    return 0;
}

int main() {
    char ch;
    char operators[] = "+-*/=;<>(){}";
    char buffer[30];
    int i = 0;

    printf("Enter your input (Ctrl+D to stop):\n");

    while ((ch = getchar()) != EOF) {
        if (strchr(operators, ch) != NULL) {
            if (i > 0) {
                buffer[i] = '\0';
                if (isKeyword(buffer)) {
                    printf("Keyword: %s\n", buffer);
                } else if (isalpha(buffer[0])) {
                    printf("Identifier: %s\n", buffer);
                } else if (isdigit(buffer[0])) {
                    printf("Number: %s\n", buffer);
                }
                i = 0;
            }
            printf("Operator: %c\n", ch);
        } 
        else if (isalnum(ch)) {
            if (i < sizeof(buffer) - 1) {
                buffer[i++] = ch;
            }
        } 
        else if ((ch == ' ' || ch == '\n' || ch == '\t') && i > 0) {
            buffer[i] = '\0';
            if (isKeyword(buffer)) {
                printf("Keyword: %s\n", buffer);
            } else if (isalpha(buffer[0])) {
                printf("Identifier: %s\n", buffer);
            } else if (isdigit(buffer[0])) {
                printf("Number: %s\n", buffer);
            }
            i = 0;
        }
    }

    if (i > 0) {
        buffer[i] = '\0';
        if (isKeyword(buffer)) {
            printf("Keyword: %s\n", buffer);
        } else if (isalpha(buffer[0])) {
            printf("Identifier: %s\n", buffer);
        } else if (isdigit(buffer[0])) {
            printf("Number: %s\n", buffer);
        }
    }

    return 0;
}

```

## INPUT:

# int a = a+b*c 

## OUTPUT:

<img width="550" height="257" alt="Screenshot 2025-09-09 134526" src="https://github.com/user-attachments/assets/dc649384-059d-4a92-939c-35e67ed7707b" />

## RESULT:
 The lexical analyzer is implemented using lex and the output is verified.
