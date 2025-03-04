# ebac-registro

#include <stdio.h>  
#include <stdlib.h> 
#include <locale.h> 
#include <string.h> 

int registro() {
    char arquivo[40];
    char cpf[40];
    char nome[40];
    char sobrenome[40];
    char cargo[40];

    printf("Registre o CPF a ser cadastrado:\n\n");
    scanf("%s", cpf);

    strcpy(arquivo, cpf);
    FILE *file = fopen(arquivo, "r");
    if (file != NULL) {
        printf("CPF já registrado.\n");
        fclose(file);
        system("pause");
        return 1;
    }

    file = fopen(arquivo, "w");
    if (file == NULL) {
        printf("Erro ao criar arquivo.\n");
        system("pause");
        return 1;
    }
    fprintf(file, ","); // inicializa o arquivo com uma vírgula para separar dados

    printf("Digite o nome a ser cadastrado:\n\n");
    scanf("%s", nome);
    fprintf(file, "%s,", nome);

    printf("Digite o sobrenome a ser cadastrado:\n\n");
    scanf("%s", sobrenome);
    fprintf(file, "%s,", sobrenome);

    printf("Digite o cargo a ser cadastrado\n\n");
    scanf("%s", cargo);
    fprintf(file, "%s\n", cargo);

    fclose(file);
    system("pause");
    return 0;
}

int consulta() {
    setlocale(LC_ALL, "portuguese");
    char cpf[40];
    char conteudo[200];

    printf("Digite o CPF a ser consultado \n\n");
    scanf("%s", cpf);

    FILE* file = fopen(cpf, "r");
    if (file == NULL) { 
        printf("Não foi possível localizar o CPF \n");
        system("pause");
        return 1;
    }

    while (fgets(conteudo, 200, file) != NULL) { 
        printf("Essas são as informações do usuário: %s\n", conteudo);
    }

    fclose(file);
    system("pause");
    return 0;
}

int deletar() {
    char cpf[40];

    printf("Digite o CPF a ser deletado:\n\n");
    scanf("%s", cpf);

    if (remove(cpf) == 0) {
        printf("Registro deletado com sucesso.\n");
    } else {
        printf("Não foi possível localizar o CPF.\n");
    }
    system("pause");
    return 0;
}

int main() {
    int opcao = 0;
    int laco = 1;

    for (laco = 1; laco == 1;) {  
        system("cls");
        setlocale(LC_ALL, "Portuguese");

        printf("### Registro Oficial da EBAC ### \n\n");
        printf("Selecione a alternativa desejada no menu: \n\n");
        printf("\t1 - Registrar nomes\n");
        printf("\t2 - Consultar nomes\n");
        printf("\t3 - Deletar nomes\n\n\n");
        printf("opção:");
        scanf("%d", &opcao);

        system("cls");

        switch (opcao) {
            case 1:
               registro();
                break;
            case 2:
                 consulta();
                break;
            case 3:
               deletar();
                break;
            default:
                printf("Esta opção não está disponível.\n\n");
                system("pause");
                break;
        }
    }
}
