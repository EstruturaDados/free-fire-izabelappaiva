#include <stdio.h>
#include <string.h>

#define MAX_ITENS 10
#define TAM_STRING 30

typedef struct {
    char nome[TAM_STRING];
    char tipo[TAM_STRING];
    int quantidade;
} Item;

int main() {
    Item mochila[MAX_ITENS];
    int total = 0;
    int opcao;

    do {
        printf("\n=== INVENTÁRIO FREE FIRE ===\n");
        printf("1 - Adicionar item\n");
        printf("2 - Remover item\n");
        printf("3 - Listar itens\n");
        printf("4 - Sair\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);
        getchar(); // limpar buffer

        switch (opcao) {

            case 1: // Adicionar item
                if (total >= MAX_ITENS) {
                    printf("Mochila cheia! Não é possível adicionar mais itens.\n");
                } else {
                    printf("\n--- Adicionar Item ---\n");

                    printf("Nome: ");
                    fgets(mochila[total].nome, TAM_STRING, stdin);
                    mochila[total].nome[strcspn(mochila[total].nome, "\n")] = '\0';

                    printf("Tipo: ");
                    fgets(mochila[total].tipo, TAM_STRING, stdin);
                    mochila[total].tipo[strcspn(mochila[total].tipo, "\n")] = '\0';

                    printf("Quantidade: ");
                    scanf("%d", &mochila[total].quantidade);
                    getchar(); // limpar \n

                    total++;
                    printf("Item adicionado com sucesso!\n");
                }
                break;

            case 2: { // Remover item
                if (total == 0) {
                    printf("A mochila está vazia. Nada para remover.\n");
                } else {
                    char nomeRemover[TAM_STRING];
                    int encontrado = 0;

                    printf("Digite o nome do item para remover: ");
                    fgets(nomeRemover, TAM_STRING, stdin);
                    nomeRemover[strcspn(nomeRemover, "\n")] = '\0';

                    for (int i = 0; i < total; i++) {
                        if (strcmp(mochila[i].nome, nomeRemover) == 0) {
                            // remover item deslocando para a esquerda
                            for (int j = i; j < total - 1; j++) {
                                mochila[j] = mochila[j + 1];
                            }
                            total--;
                            encontrado = 1;
                            printf("Item removido com sucesso!\n");
                            break;
                        }
                    }

                    if (!encontrado)
                        printf("Item não encontrado.\n");
                }
                break;
            }

            case 3: // Listar itens
                if (total == 0) {
                    printf("A mochila está vazia.\n");
                } else {
                    printf("\n=== ITENS NA MOCHILA ===\n");
                    printf("%-20s %-15s %-10s\n", "Nome", "Tipo", "Quantidade");
                    printf("----------------------------------------------\n");

                    for (int i = 0; i < total; i++) {
                        printf("%-20s %-15s %-10d\n",
                               mochila[i].nome,
                               mochila[i].tipo,
                               mochila[i].quantidade);
                    }
                }
                break;

            case 4:
                printf("Saindo...\n");
                break;

            default:
                printf("Opção inválida!\n");
        }

    } while (opcao != 4);

    return 0;
}