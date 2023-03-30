# #include <stdio.h>
#include <string.h>
#define MAX_PRODUCTS 100 // 최대 상품 수

struct Product {
    char name[50];
    int price;
    int quantity;
};

struct Inventory {
    struct Product products[MAX_PRODUCTS];
    int count;
};

void add_product(struct Inventory* inventory) {
    if (inventory->count == MAX_PRODUCTS) {
        printf("재고 추가 불가능: 최대 상품 수 초과\n");
        return;
    }

    struct Product new_product;

    printf("새 상품 이름: ");
    scanf("%s", new_product.name);

    printf("새 상품 가격: ");
    scanf("%d", &new_product.price);

    printf("새 상품 개수: ");
    scanf("%d", &new_product.quantity);

    inventory->products[inventory->count] = new_product;
    inventory->count++;

    printf("새 상품이 추가되었습니다.\n");
}

void print_inventory(struct Inventory inventory) {
    printf("현재 재고 목록:\n");

    for (int i = 0; i < inventory.count; i++) {
        printf("%s (가격: %d원, 개수: %d개, 총재고액: %d원)\n",
               inventory.products[i].name,
               inventory.products[i].price,
               inventory.products[i].quantity,
               inventory.products[i].price * inventory.products[i].quantity);
    }
}

void search_product(struct Inventory inventory) {
    char search_name[50];

    printf("검색할 상품 이름: ");
    scanf("%s", search_name);

    for (int i = 0; i < inventory.count; i++) {
        if (strcmp(search_name, inventory.products[i].name) == 0) {
            printf("%s (가격: %d원, 개수: %d개, 총재고액: %d원)\n",
                   inventory.products[i].name,
                   inventory.products[i].price,
                   inventory.products[i].quantity,
                   inventory.products[i].price * inventory.products[i].quantity);
            return;
        }
    }

    printf("일치하는 상품이 없습니다.\n");
}

int main(void) {
    struct Inventory inventory = { .count = 0 };

    while (1) {
        int menu;

        printf("\n1. 상품 추가\n");
        printf("2. 재고 검색\n");
        printf("3. 재고 목록 출력\n");
        printf("4. 종료\n");
        printf("메뉴 선택: ");
        scanf("%d", &menu);

        switch (menu) {
            case 1:
                add_product(&inventory);
                break;
            case 2:
                search_product(inventory);
                break;
            case 3:
                print_inventory(inventory);
                break;
            case 4:
                printf("프로그램을 종료합니다.\n");
                return 0;
            default:
                printf("잘못된 입력입니다.\n");
                break;
        }
    }
}
