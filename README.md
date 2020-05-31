
#include <stdio.h>
#include <stdlib.h>

FILE* AbreArquivo(char modo, char caminho[30]){
    FILE *arquivo;
    switch(modo){
        case 'g':
            arquivo = fopen(caminho,"wt");
            break;
        case 'l':
            arquivo = fopen(caminho,"rt");
            break;
        case 'a':
            arquivo = fopen(caminho,"a");
            break;
            
            
    }
    if(arquivo==NULL){      //Se haver algum erro, o ponteiro apontará para NULL
        printf("Nao foi possivel abrir o arquivo");
        exit(0);
    }
    return arquivo;
}
void FecharArquivo(FILE *arquivo){
    fclose(arquivo);
}

void registo(char nome[30], int telefone){
    FILE *arquivo;
    arquivo = AbreArquivo('a', "agenda.txt");
    fprintf(arquivo, "%s %d\n", nome, telefone);
    FecharArquivo(arquivo);
}

void Lista(){
    FILE *arquivo;
    char nome[30];
    int telefone;

    arquivo = AbreArquivo('l',"agenda.txt");

    while(!feof(arquivo)){
        fscanf(arquivo,"%s %d ", &nome, &telefone);
        printf("Nome: %s  -  Telefone: %d\n", nome, telefone);
    }
    FecharArquivo(arquivo);
}

int main(){
    int opcao;
    char nome[30];
    int telefone;
    do{
       // system("cls");
        printf("\n\n\t\tBem Vindo ao programa AGENDA\n");
        printf("\nMENU");
        printf("\n 1 - Registo Nome e telefone");
        printf("\n 2 - Lista de todos os Nomes e telefones");
        printf("\n 3 - Sair");
         //  printf("\n 4 -pesquisar  todos os Nomes e telefones");
        printf("\nDigite uma opcao: ");
        scanf("%d", &opcao);
       // system("cls");

        switch(opcao){
            case 1:
                printf("\nDigite o teu nome: ");
              
               scanf("%s",nome);
                printf("\nDigite o telefone: ");
                scanf("%d", &telefone);
                registo(nome, telefone);
                //system("pause");
                break;
            case 2:
                Lista();
                //system("pause");
                break;
            case 3:
                printf("\n\nFinalizar...\n\n");
                //system("pause");
                exit(0);
                break;
 default:
                printf("\n\nOpcao invalida! Tente Novamente!\n\n");
                //system("pause");

        }
    }while(opcao!=3);

    return 0;
}
