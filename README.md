# miniproject
#include<string.h>
#include<stdio.h>
#include<conio.h>
 void main()
 {
     struct symtab
{
    char lables[20];
    int value;
};
     struct symtab s[10];
     char label[20],mnemonic[20],operand[20];
     int locctr=1000,n,i,a=0,j=0;
     int temp;
     FILE *fp, *fptr;

     printf(" *********assembler*********: \n \n ");
     printf(" \t\t\t\t***assembler manual***\t\t\t\t \n\n ");
     printf("mnemonics defined for assembler are \n \n");
     printf(" LDA \n STA \n STL \n COMP \n JEQ \n LDCH \n JLT \n ADD \n SUB \n STX \n \n");
     printf("lables defined for assembler are \n \n");
     printf(" LAB1 \n LAB2 \n  LAB3 \n LAB4 \n LAB5 \n LAB6 \n \n ");
     printf("use defined lable as operand \n");
     printf(" for no label please use '-' special symbol \n ");
     printf(" program in assembly language \n");

     fp=fopen("d:\\temp.txt","w");
     printf(" \n enter no. of instruction u want to write");
     scanf("%d",&n);
     for(i=0;i<n;i++)
     {
         a:
               scanf("%s\t%s\t%s",label, mnemonic,operand);
               if(strcmp(label,"lab1")==0 || strcmp(label,"lab2")==0 || strcmp(label,"lab3")==0 || strcmp(label,"lab4")==0 || strcmp(label,"lab5")==0 || strcmp(label,"lab6")==0 ||
                  strcmp(label,"lab6")==0 ||strcmp(label,"-")==0)
               {
               if (strcmp(mnemonic,"lda")==0 || strcmp(mnemonic,"sta")==0 ||strcmp(mnemonic,"stl")==0 ||strcmp(mnemonic,"comp")==0 ||strcmp(mnemonic,"jeq")==0 ||strcmp(mnemonic,"ldx")==0
                ||strcmp(mnemonic,"ldch")==0 ||strcmp(mnemonic,"jlt")==0 ||strcmp(mnemonic,"add")==0 ||strcmp(mnemonic,"sub")==0 ||strcmp(mnemonic,"stx")==0)



                  {
                   if(strcmp(operand,"lab1")==0 || strcmp(operand,"lab2")==0 || strcmp(operand,"lab3")==0 || strcmp(operand,"lab4")==0 || strcmp(operand,"lab5")==0 || strcmp(operand,"lab6")==0 ||
                  strcmp(operand,"lab6")==0 )
                  {

             fprintf(fp,"%d\t%s\t%s\t%s\n",locctr,label,mnemonic,operand);
             strcpy(s[i].lables,label);
             s[i].value=locctr;
            locctr=locctr+3;
                  }
                 else
               {
                   printf("operand not defined for assembler \n");
                   printf("please use apropriate operand \n \n");
                   goto a;
               }
                  }
               else
               {
                   printf("mnemonic not defined for assembler \n");
                   printf("please use apropriate mnemonic \n \n");
                   goto a;
               }
           }
          else
             {

              printf(" label not defined in assembler \n");
              printf("please input appropriate lable \n \n");
              goto a;
          }
     }
     fclose(fp);
     fptr=fopen("d:\\symtab.txt","w");
     printf("symtab is:\n ");
     for(i=0;i<n;i++)
     {
         printf("%s\t\t%d",&s[i].lables,s[i].value);
         fprintf(fp,"%s\t\t%d",&s[i].lables,s[i].value);
         printf("\n");
     }
     fclose(fp);

      getch();
 }
