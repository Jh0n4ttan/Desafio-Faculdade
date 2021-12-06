# Desafio-Faculdade
# Desafio feito para um trabalho
#include <stdio.h>
#include <stdlib.h>
#include <locale.h>
#define TAM 20

/* Prototipos de sub-rotinas. */
void ORDENA_CRES (int vet[], int faixa);

/* Prototipos de funcoes */
float MEDIANA (int vet[], int faixa);
int *MODA (int vet[], int faixa);
int CONTA_ELEM (int vet[], int faixa);

int main (void)
{

  {
   system("cls");
   printf("\n ------------------ Medidas de Posição e Dispersão para dados dispersos ------------- ");
   printf("\n ------------------ Jhonatan Mello -------------------------------------------------- ");
   }

  int vetor[TAM];
  float soma=0,mediana, media,moda;
  register int i;
  int qtd, n, auxiliar;
  int *v_moda = NULL;


  do
  {
    printf("\n\n !Quantidade maxima ate 20 elementos!");
    printf ("\n\n Informe a quantidade de elementos: ");
    scanf  ("%d", &qtd);

    if (qtd > TAM)
      printf ("\n Tamanho maximo excedido = 20.\n");

  } while (qtd > TAM);


  for (i = 0; i < qtd; i++)
  {
    printf ("\n Digite o valor do numero : ", i);
    scanf  ("%d", &vetor[i]);

	soma=soma+vetor[i];
  }

   media = soma/qtd;

    printf("\n Media: %.1f",media);


  mediana =  MEDIANA (vetor, qtd);

  printf ("\n\n Mediana = %.1f\n", mediana);

  printf ("\n\n Moda: ", moda);

  n = CONTA_ELEM (vetor, qtd);

  v_moda = MODA (vetor, qtd);


  for (i = 0; i < n; i++)
    printf ("\t%d", *(v_moda + i) );

  return (0);
}


/* Sub-rotina para ordenar elementos de um
  vetor de forma crescente */
void ORDENA_CRES (int vet[], int faixa)
{
  register int i, j;
  int aux;

  for (i = 0; i < (faixa - 1); i++)
    for (j = i + 1; j < faixa; j++)
      if (vet[i] > vet[j])
      {
        aux = vet[i];
        vet[i] = vet[j];
        vet[j] = aux;
      }
}

/* Funcao que retorna o valor da mediana de um
  vetor de numeros de ponto flutuante */


float MEDIANA (int vet[], int faixa)
{
  register int i; /* indexadores com tipo register
                    dao mais ganho de performance no processamento
                    pois sao armazenados em registradores. */
  float m1, m2;


  ORDENA_CRES (vet, faixa); // Ordenando conjunto numerico.

  puts ("");
  for (i = 0; i < faixa; i++)
    printf ("%5d", vet[i]);


  switch (faixa % 2) // Seletor para calculo da mediana.
  {
    case 0: // Faixa de valores (qtd de elem do vetor) e PAR.
      m1 = vet[faixa / 2 - 1];
      m2 = vet[faixa / 2];
      m1 += m2;
      return  (m1 / 2);

    case 1: // Faixa de valores do vetor e IMPAR.
      m1 = vet[ (faixa - 1) / 2 ];
      return m1;
  }
}

int CONTA_ELEM (int vet[], int faixa)
{
  int x;
  register int i, j;
  int flag;

  x = 0;
  flag = 0;

  for (i = 0, j = i + 1; i < (faixa - 1); i ++, j++)
  {
    if (vet[i] == vet[j])
    {
      if (flag == 0)
      {
        x++;
        flag = 1;
      }
    }
    else
      flag = 0;

  }
  return (x);
}

int *MODA (int vet[], int faixa)
{
  /*int moda[faixa];  Este vetor usando alocacao estatica e visto como variavel local
                        pelo compilador e nao pode ser retornado pela funcao pois ao terminar
                        a execucao da mesma ele e destruido. */

  int n, flag;
  int *moda;
  register int i, j, k;

  n = CONTA_ELEM (vet, faixa); // Retorna a quantidade de elementos repetidos no vetor.

  moda = (int *) malloc (n * sizeof (int) );  /* Este vetor com alocacao dinamica pode
                                                       ser retornado pois ele so e desalocado
                                                       quando se usa o comando free(); */


  k = flag = 0;


  for (i = 0, j = i + 1; i < (faixa - 1); i++, j++)
  {
    if (vet[i] == vet[j])
    {
      if (flag == 0)
      {
        moda[k++] = vet[j];
        flag = 1;
      }
    }
    else
      flag = 0;
  }

  return moda;
}
