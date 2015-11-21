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
   struct assembler
  {
    char label[20];
    char mnemonic[20];
    char operand[20];
  };
  struct object_code
 {
	char opcode[10];
	int adrs;
 };
     struct object_code ob[10];
     struct symtab s[10];
     struct assembler asmb[20];
     char prog_name[10],opcode;
     int locctr,n,i,c=0,d,first_time_copy=0,add,text_record_length=0,text;
     int temp,j=0,symtab_entry=0,k,size_of_symtab=0,starting_address,ending_address,program_length;
     char temp_mnemonic[6],a[10],ch1[20],ch2[20],ch3[20];
     FILE *fp, *fptr,*fpp;

     printf("\n\n *********SIC ASSEMBLER*********\n \n ");
     printf(" \t\t\t\t***assembler manual***\t\t\t\t \n\n ");
     printf("Mnemonics defined for assembler are \n \n");
     printf(" LDA \n STA \n LDL \n STL \n COMP \n JEQ \n LDCH \n JLT \n ADD \n SUB \n STX \n J \n TIX \n RESW \n RESB 	 \n");
     printf("Lables defined for assembler are \n \n");
     printf(" LAB1 \n LAB2 \n LAB3 \n LAB4 \n LAB5 \n LAB6 \n CLOOP \n ENDFIL \n THREE \n ZERO \n RETADR \n LENGTH \n MAXLEN \n WLOOP \n \n ");
     printf("Use defined lable as operand \n");
     printf(" For no label please use '-' special symbol \n \n");
     printf("OBJECT CODE/MACHINE CODE FORMAT (IN HEX) IS  : \n\n ");
     printf("OPCODE(2 BIT) ADDRESS(4 BIT) \n\n");
     printf(" program in assembly language \n");

     fp=fopen("d:\\intermediate_file.txt","w");
    
     printf(" \n Enter no. of instruction you want to write");
     scanf("%d",&n);
     printf("enter program name \n");
      scanf("%s",prog_name);
      printf("please input starting address\n");
      scanf("%x",&locctr);
      printf("%s ",prog_name);
     printf("START ");
     printf("%x\n",locctr);
     starting_address=locctr;
     for(i=0;i<n;i++)
     {
         d:
         	    c=0;
         	     fpp=fopen("d:\\OPTAB.txt","r");
               scanf("%s\t%s\t%s",asmb[i].label, asmb[i].mnemonic,asmb[i].operand);
               
               if(strcmp(asmb[i].label,"LAB1")==0 || strcmp(asmb[i].label,"LAB2")==0 || strcmp(asmb[i].label,"LAB3")==0 || strcmp(asmb[i].label,"LAB4")==0 || strcmp(asmb[i].label,"LAB5")==0 || strcmp(asmb[i].label,"LAB6")==0 ||
                  strcmp(asmb[i].label,"CLOOP")==0 ||strcmp(asmb[i].label,"ENDFIL")==0 || strcmp(asmb[i].label,"THREE")==0 || strcmp(asmb[i].label,"ZERO")==0 || 
                  strcmp(asmb[i].label,"RETADR")==0  || strcmp(asmb[i].label,"LENGTH")==0 || strcmp(asmb[i].label,"MAXLEN")==0 || strcmp(asmb[i].label,"-")==0 || strcmp(asmb[i].label,"WLOOP")==0 ) 
               {
                    while(!feof(fpp))
                    {

                       	fscanf(fpp,"%s  %s",temp_mnemonic,a);
                       	if(strcmp(temp_mnemonic,asmb[i].mnemonic)==0)
                       	{
                       		c=1;
                       		break;
                       	}
                       	
                    }
                        if(c==0)
                        {
                       	printf("\n Mnemonics not defined in assembler \n");
                       	printf("  Please input mnemonic which is defined in assembler \n");
                         fclose(fpp);
                       	goto d;
                        }
                       
                if(strcmp(asmb[i].mnemonic,"RESW")==0 || strcmp(asmb[i].mnemonic,"RESB")==0  )  
                goto asmb_label2;
                       
                   if(strcmp(asmb[i].operand,"LAB1")==0 || strcmp(asmb[i].operand,"LAB2")==0 || strcmp(asmb[i].operand,"LAB3")==0 || strcmp(asmb[i].operand,"LAB4")==0 || strcmp(asmb[i].operand,"LAB5")==0 || strcmp(asmb[i].operand,"LAB6")==0 ||
                  strcmp(asmb[i].operand,"LAB6")==0 ||  strcmp(asmb[i].operand,"CLOOP")==0 ||  strcmp(asmb[i].operand,"ENDFIL")==0 || strcmp(asmb[i].operand,"THREE")==0  ||  strcmp(asmb[i].operand,"ZERO")==0 ||
				    strcmp(asmb[i].operand,"RETADR")==0  ||  strcmp(asmb[i].operand,"LENGTH")==0  ||  strcmp(asmb[i].operand,"MAXLEN")==0  ||   strcmp(asmb[i].operand,"WLOOP")==0 || strcmp(asmb[i].operand,"-") ==0)
                  {
      asmb_label2:  
	                 
                   if(strcmp(asmb[i].label,"-")!=0)
                     {
                      if(first_time_copy==0)
                      {
             	        fprintf(fp,"%x\t%s\t%s\t%s\n",locctr,asmb[i].label,asmb[i].mnemonic,asmb[i].operand);
                        strcpy(s[j].lables,asmb[i].label);
                        s[j].value=locctr;
                        first_time_copy=1;
                        j++;
                        size_of_symtab++;
                      }
                     else
                     {
                        for(k=0;k<size_of_symtab;k++)
                       {
              	           symtab_entry=1;
            
              	           if(strcmp(asmb[i].label,s[k].lables)==0)
              	        {
              		          printf("lable defined in symtab \n");
              		          printf("please input apropriate lable \n\n");
              		          goto d;
              		          break;
              	        }
                       }
                          if(symtab_entry==1)
                         {
              	            fprintf(fp,"%x\t%s\t%s\t%s\n",locctr,asmb[i].label,asmb[i].mnemonic,asmb[i].operand);
              	             strcpy(s[j].lables,asmb[i].label);
              	             s[j].value=locctr;
                           	  size_of_symtab++;
              	              j++;
                         }
                    }
                         if(strcmp(asmb[i].mnemonic,"RESB")==0)
                         {
            	            locctr=locctr+atoi(asmb[i].operand);
                         }
                         else if(strcmp(asmb[i].mnemonic,"RESW")==0)
                         {
            	            locctr=locctr+3*atoi(asmb[i].operand);
                         }
                         else
                         {
                          locctr=locctr+3;
                         }
                 
                    }
                    
                 else
                 {
        	           fprintf(fp,"%x\t%s\t%s\t%s\n",locctr,asmb[i].label,asmb[i].mnemonic,asmb[i].operand);
        	           
		               if(strcmp(asmb[i].mnemonic,"RESB")==0)
                      {
            	        locctr=locctr+atoi(asmb[i].operand);
                      }
                      
                     else if(strcmp(asmb[i].mnemonic,"RESW")==0)
                     {
            	        locctr=locctr+3*atoi(asmb[i].operand);
            	     }
                     else
                    {
        	          locctr=locctr+3;
                    }
                }
        
                 }
                 
                 else
                 {
                   printf("operand not defined for assembler \n");
                   printf("please use apropriate operand \n\n");
                   goto d;
                 }
               
              }
              
                else
                {
                   printf(" label not defined in assembler \n");
                   printf("please input appropriate lable \n\n");
                   goto d;
                }
     }

     fclose(fpp);
     fclose(fp);
     
     ending_address=locctr;
      printf(" END");
     printf("\t%x",locctr);
     program_length= (ending_address-starting_address);
     
     fp=fopen("d:\\intermediate_file.txt","r");
     
      printf(" \n \n AFTER ADDRESSING THE INTERMEDIATE FILE IS:\n");
      while(fscanf(fp,"\t%x\t%s\t%s\t%s",&add,ch1,ch2,ch3)!=EOF)
     {
     	printf("\n%x\t%s\t%s\t%s\n\n",add,ch1,ch2,ch3);
     }
     
      fclose(fp); 
     
     printf("\n symtab is: \n\n");
     for(j=0;j<size_of_symtab;j++)
     {
     	printf("%s\t%x\n",s[j].lables,s[j].value);
     	printf("\n");
     }
     printf("\n\n");
     
     fptr=fopen("d:\\intermediate_file.txt","r");
     fpp=fopen("d:\\OPTAB.txt","r");
     fp=fopen("d:\\object_program.txt","w");
     fprintf(fp,"H^");
     fprintf(fp,"%s^",prog_name);
     fprintf(fp,"%x^%d\n",starting_address,program_length);
     
     i=0;
    printf("\t\t step 2\n\n ");
    printf("machine code(in hex) is:\n\n");
    fprintf(fp,"T");
     while(fscanf(fptr,"\t%x\t%s\t%s\t%s",&add,ch1,ch2,ch3)!=EOF)
     {
     	printf("%x\t%s\t%s\t%s",add,ch1,ch2,ch3);
     	if(strcmp(ch2,"RESW")==0 || strcmp(ch2,"RESB")==0 )
     	{
     		printf("\n\n NO MACHINE CODE  \n ");
     		strcpy(ob[i].opcode,"noopcode");
     	}
     	else
     	{
     	   while(!feof(fpp))
     	   {
     		fscanf(fpp,"%s\t%s",temp_mnemonic,a);
     	
     		   if(strcmp(temp_mnemonic,ch2)==0)
     		   {
     			 printf("\n\n%s",a);
     			 strcpy(ob[i].opcode,a);
     			 ob[i].adrs=1;
     			 break;
     		   }
     	   }
     	     rewind(fpp);
     		for(j=0;j<size_of_symtab;j++)
     	    {
     		    if(strcmp(ch3,s[j].lables)==0)
     		    {
     		       printf("%x\n",s[j].value);
     			   ob[i].adrs=s[j].value;
     			    break;
     		    }
     		}
        }
     	i++;
     	
     	printf("\n");
     }

      j=0;
     while(j<i)
     {
		 if(strcmp(ob[j].opcode,"noopcode")==0)
		 {
		     j++;
		 }
		 else
		 { 
		 if(strcmp(ob[j-1].opcode,"noopcode")==0 && j!=0)
	     {
	     	fprintf(fp,"\nT");
		 }
		    fprintf(fp,"^%s%x",ob[j].opcode,ob[j].adrs);
		    j++;
        }
     }
 
     fprintf(fp,"\nE^");
     fprintf(fp,"%x",starting_address);
	 fclose(fptr);
	 fclose(fpp);
	 fclose(fp);
	 printf("\n STEP 3:\n");
	 printf(" \n\n OBJECT FILE WRITTEN \n");
	 getch();
 }

