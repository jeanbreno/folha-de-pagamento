# folha-de-pagamento
Exercício para criar uma folha de pagamento na linguagem C. 


#include <stdio.h>
#include <stdlib.h>
#include <locale.h>



/* 
		Programa para gerar folha de pagamento.  
		Jean Breno - 20201101602 - UVA
	
		Tabela INSS: https://www.inss.gov.br/servicos-do-inss/calculo-da-guia-da-previdencia-social-gps/tabela-de-contribuicao-mensal/
		
		Tabela IRRF: https://www.debit.com.br/tabelas/tabelas-irrf.php
					https://blog.convenia.com.br/como-calcular-irrf-na-folha-de-pagamento/
					
		Alíquota FGTS: https://extra.globo.com/noticias/economia/mudanca-do-salario-minimo-como-ficam-as-contribuicoes-do-fgts-do-inss-24192569.html


*/
	float calculoFGTS(float salario1, float fgts1);
	float calculoINSS(float salario2, float inss2);
	float calculoIRRF(float salario3, float irrf3, float inss3);


int main()

{
	setlocale(LC_ALL, "");
	system("color 1F");
	setbuf(stdin,NULL);
	char empresa[50], nome[100], cargo[100], mesRef[20], cnpj[14];
	int  repetir, play, codigo, anoRef, refSalario, percentualFGTS, faixaIRRF;
	float salario, fgts, inss, irrf, percentualINSS, percentualIRRF;
	
	
	
	printf("---------------------------------------------------------------------------\n");
	printf("---------------------------------------------------------------------------\n");
	printf("---------------------------------------------------------------------------\n");
	printf("--------------------SISTEMA PARA GERAR FOLHA DE PAGAMENTO------------------\n");
	printf("---------------------------------------------------------------------------\n");
	printf("---------------------------------------------------------------------------\n");
	printf("---------------------------------------------------------------------------\n\n");
	printf("----------------- Digite [1] para começar ou [0] para sair ---------------- ");
	printf("\n\n\t\t Escolha: ");
		scanf("%d", &play); fflush(stdin);
		
		while (play != 1 && play != 0)
			{
				system("color 4F");
				printf("\n\t\t\t Opção inválida! \n\t\t\t Digite novamente! " );
				printf("\n\n\t\t Digite [1] para começar ou [0] para sair ");
				printf("\n\n\t\t Escolha: ");
					scanf("%d", &play); fflush(stdin);
			}
			
	
		while (play == 1) 
			{
				system("color 1F");
				printf("\n---------------------------------------------------------------------------\n");
				printf("\n\tDigite o nome da empresa: ");
					gets(empresa); strupr(empresa); fflush(stdin);
				
				printf("\n\tMês de referência da folha de pagamento(Por extenso): ");
					gets(mesRef); strupr(mesRef); fflush(stdin);
					
				printf("\n\tAno de referência da folha de pagamento(AAAA): ");
					scanf("%d", &anoRef); fflush(stdin);
					
				printf("\n\tCNPJ da empresa(Somente números): ");
					gets(cnpj); fflush(stdin);
					
				printf("\n\tCódigo do funcionário(1234): ");
					scanf("%d", &codigo); fflush(stdin);
					
				printf("\n\tNome do funcionário: ");
					gets(nome); strupr(nome); fflush(stdin);
					
				printf("\n\tCargo do(a) %s: ", nome);
					gets(cargo); strupr(cargo);fflush(stdin);
						
				printf("\n\tReferência para o salário(Em dias): ");
					scanf("%d", &refSalario); fflush(stdin);
							
				printf("\n\tQual o salário bruto do(a) %s: R$ ", nome);
					scanf("%f", &salario); fflush(stdin);
					
					
				fgts = calculoFGTS(salario, fgts);
				inss = calculoINSS(salario, inss);
				irrf = calculoIRRF(salario, irrf, inss);
				percentualFGTS = 8;
				
				if (salario <= 1045.00 )
				{ 
				 percentualINSS = 7.5 ;
				}
				else
					if (salario <= 2089.60)
						{
						percentualINSS = 9 ;	
						}
						else
							if (salario <= 3134.40)
								{
								percentualINSS = 12 ;
								}
								else
									if (salario <= 6101.06)
										{
										percentualINSS = 14 ;
										}
				
				if (salario <= 1903.98)
				{
				percentualIRRF = 0;
				faixaIRRF = 0;
				}
				else
					if (salario <= 2826.65)
						{
						percentualIRRF = 7.5;
						faixaIRRF = 1;
						}
						else
							if (salario <= 3751.05)
								{
								percentualIRRF = 15;
								faixaIRRF = 2;
								}
								else
									if (salario <= 4664.68)
										{
										percentualIRRF = 25;
										faixaIRRF = 3;
										}
										else
											if (salario > 4664.68)
												{
												percentualIRRF = 27.5;
												faixaIRRF = 4;
												}
				
				printf("\n\n\n ---------------------- RECIBO DE PAGAMENTO DE SALÁRIO ----------------------\n");
				printf("\n\t %s ", empresa);
				printf("\n\t %s               %s- %d ", cnpj, mesRef, anoRef);
				printf("\n\n\t CÓDIGO: %d ", codigo);
				printf("\t NOME DO FUNCIONÁRIO: %s ", nome) ;
				printf("\n\t CARGO: %s \n\n\n ", cargo);		
				
				printf(" --- Descrição ------ Referência ------ Vencimentos ------ Descontos ------ \n");
				printf("      SALÁRIO           %d dias          R$ %.2f \n", refSalario, salario);
				printf("      INSS              %.1f %%                               R$ %.2f \n", percentualINSS, inss);
				printf("      IRRF              %.1f %%                               R$ %.2f \n", percentualIRRF, irrf);
		
				printf("\n\n\n\n\n\tFGTS: %d %% --- R$ %.2f ", percentualFGTS, fgts);
				printf("\n\tSALÁRIO BASE PARA CÁLCULO IRRF: %.2f", salario - inss );
				printf("\t  ---  FAIXA IRRF: %d", faixaIRRF);
				printf("\n\tSALÁRIO BRUTO: R$ %.2f", salario);
				printf("\n\tSALÁRIO LÍQUIDO: R$ %.2f\n", salario - inss - irrf);
				printf("\n\n---------------------------------------------------------------------------\n\n");
	
				
				printf("\n\t Deseja criar outra folha de pagamento? \n\n\t [1] Sim \n\t [0] Não");
				printf("\n\t Escolha: ");
					scanf("%d", &play);	fflush(stdin);	
					while (play <0 || play >1)
					{
						system("color 4F");
						printf("\n\t\t\t Opção inválida! \n\t\t\t Digite novamente! " );
						printf("\n\n\t Digite [1] para Sim ou [0] para Não ");
						printf("\n\t Escolha: ");
							scanf("%d", &play); fflush(stdin); setbuf(stdin, 0);
							
					 } 
					 
				
		}
		
		if (play == 0)
			{
				system("color 0F");
				printf("");
				printf("\n\n\t\t Ok... Até a próxima! ");
				printf("");

				return;
			}
			
		
		
		
system ("\n\npause\n\n");		
return;
}


float calculoFGTS(float salario1, float fgts1)
	{	
	fgts1 = salario1 * 0.08;
	return fgts1 ;
	}

float calculoINSS(float salario2, float inss2)
{
	if (salario2 <= 1045.00 )
		{ 
		inss2 = salario2 * 0.075 ;
		return inss2;
		}
		else
			if (salario2 <= 2089.60)
				{
				inss2 = salario2 * 0.09 ;	
				return inss2;
				}
				else
					if (salario2 <= 3134.40)
						{
						inss2 = salario2 * 0.12 ;
						return inss2;
						}
						else
							if (salario2 <= 6101.06)
								{
								inss2 = salario2 * 0.14 ;
								return inss2;
								}
}

float calculoIRRF(float salario3, float irrf3, float inss3)
{
	if (salario3 <= 1903.98)
		{
		irrf3 = 0 ;
		return irrf3;
		}
		else
			if (salario3 <= 2826.65)
				{
				irrf3 = (salario3 - inss3) * 0.075 - 142.80 ;
				return irrf3;
				}
				else
					if (salario3 <= 3751.05)
						{
						irrf3 = (salario3 - inss3) * 0.15 - 354.80 ; 
						return irrf3;
						}
						else
							if (salario3 <= 4664.68)
								{
								irrf3 = (salario3 - inss3) * 0.225	- 636.13 ;
								return irrf3;
								}
								else
									if (salario3 > 4664.68)
										{
										irrf3 = (salario3 - inss3) * 0.275 - 869.36 ;
										return irrf3;	
										}
}



/*
Tentativa de criar uma função para o usuário digitar apenas números.
char limiteCnpj (char *c, char *cnpj, int a, double d)
{
	
	do {	
		int a=0;
		char c, cnpj[14];
		double d;
		
			c = getch();         //Armazena o que foi digitado na variável c
	       if (isdigit(c) && a < 14)
		   		{         //isdigit(c) analisa se c é um dígito - número
		           cnpj[a]=c;
		           printf("%c",cnpj[a]);
		           a++; 
	           }
		       else if( c==8 && a)
			   	{         //8 é o Back Space na tabela ASCII
		           a--;
		           cnpj[a]='\0';
		           printf("\b \b");    //Apagando o que foi digitado pelo Usuário
		           }
       				else if 
					   (c != 13) printf("\a");        //Soa um beep
       	
	   }
	   while( c!=13 );    //13 é o ENTER na tabela ASCII
	   
	    cnpj[a]='\0';
		d=atol(cnpj);
		return d;
		
}
*/
