%{
#include <stdio.h>
#include <stdlib.h>
int binary_to_decimal(const char *binary);
%}

%%
[01]+   {
            int decimal = binary_to_decimal(yytext);
            printf("Binary: %s -> Decimal: %d\n", yytext, decimal);
        }
.|\n    ; // Ignore other characters
%%

int binary_to_decimal(const char *binary) {
    int decimal = 0;
    while (*binary) {
        decimal = decimal * 2 + (*binary - '0');
        binary++;
    }
    return decimal;
}

int main(int argc, char **argv) {
    yylex();
    return 0;
}
