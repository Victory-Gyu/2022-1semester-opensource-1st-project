# 2022-1semester-opensource-1st-project

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#pragma warning(disable:4996)


#define SIZE   20
#define SAFE_FREE(p) if(p) { free(p); p=NULL; }



typedef struct
{
    char name[20];		// 이름
    int number;	// 학년
    char yesno[20];		// 코로나 증상 유무
    char major[20];	// 학과
} colona; // struct 선언



void menu_print();
void insert(colona* ptr, int* location);
void delete_info(colona* ptr, int* location, char* name);
void search(colona* ptr, int* location, char* name);
void colonalist(colona* ptr, int* location);



int main(void)
{
    int menu, index = 0;                                 
    char* name = (char*)malloc(sizeof(char) * SIZE);         // 이름 동적 메모리 할당



     // struct동적 메모리 할당
    colona* ptr = (char*)malloc(sizeof(colona) * SIZE);



    while (1)
    {
        menu_print();
        scanf("%d", &menu);



        switch (menu) // 
        {
        case 1: insert(ptr, &index);  break;
        case 2: search(ptr, &index, name); break;
        case 3: colonalist(ptr, &index);   break;
        case 4: printf("종료합니다.\n\n");    exit(0);
        default: printf("잘못된 입력입니다.\n\n");  break;
        }
    }



    SAFE_FREE(name); // 동적 메모리 해제
    SAFE_FREE(ptr);  // 동적 메모리 해제



    return 0;
}



void menu_print() // 메뉴 출력
{
    printf("\n<충북대학교 전자정보대학 코로나 확진 관리 프로그램>\n");
    printf("1. 학생 정보 입력 \n");
    printf("2. 검색 \n");
    printf("3. 목록 출력 \n");
    printf("4. 종료 \n");
    printf("번호를 입력하시오: ");
}



void insert(colona* ptr, int* location) // 데이터 삽입
{
    printf("추가할 정보를 입력하세요\n");

    if (*location < SIZE)
    {
        printf(" 이름 : "); scanf(" %s", &ptr[*location].name);
        printf(" 학번 : "); scanf("%d", &ptr[*location].number);
        printf(" 학과(전기공학과:A, 전자공학과:B, 정보통신공학부:C, 컴퓨터공학과:D, 소프트웨어학부:E, 지능로봇공학과:F): "); scanf(" %s", &ptr[*location].major);
        printf(" 코로나 증상유무(o/x) : "); scanf(" %s", &ptr[*location].yesno);
       
       
        (*location)++;
    }
    
}





void search(colona* ptr, int* location, char* name) // 데이터 검색
{
    int i;
    printf("\n이름을 입력하세요 : ");



    memset(name, '\0', SIZE);
    fflush(stdin); // 키보드 입력 버퍼 비우기
    fgets(name, SIZE, stdin);
    *(name + (strlen(name) - 1)) = '\0';
     scanf(" %s", name);



    printf("\n--------검색 결과----------\n");


    for (i = 0; i < (*location); ++i)
    {
        if (!strcmp(ptr[i].name, name))
        {
            printf(" %5s   %5d   %5s   %5s   \n", ptr[i].name, ptr[i].number, ptr[i].major, ptr[i].yesno);
        }

    }
    printf("-------------------------------\n\n");
}



void colonalist(colona* ptr, int* location) // 데이터 리스트 출력
{
    int i;



    if (*location > 0)
    {

        printf("----------------------------------------------------\n");
        printf("    이름      학번       학과    코로나 증상 유무   \n");
        printf("----------------------------------------------------\n");

        for (i = 0; i < (*location); ++i)
        {
            printf("[%d] %5s %7d     %7s        %7s \n", i + 1, ptr[i].name, ptr[i].number, ptr[i].major, ptr[i].yesno);
        }
        int countA = 0;
        int countB = 0;
        int countC = 0;
        int countD = 0;
        int countE = 0;
        int countF = 0;
        for (i = 0; i < (*location); ++i)
        {
            if (*ptr[i].major == 'A' && *ptr[i].yesno == 'o')
            {
                countA += 1;
            }
            if (*ptr[i].major == 'B' && *ptr[i].yesno == 'o')
            {
                countB += 1;
            }
            if (*ptr[i].major == 'C' && *ptr[i].yesno == 'o')
            {
                countC += 1;
            }
            if (*ptr[i].major == 'D' && *ptr[i].yesno == 'o')
            {
                countD += 1;

            }
            if (*ptr[i].major == 'E' && *ptr[i].yesno == 'o')
            {
                countE += 1;
            }
            if (*ptr[i].major == 'F' && *ptr[i].yesno == 'o')
            {
                countF += 1;

            }
        }
        printf("현재 전자정보대학교 코로나 확진자: %d\n", countA+countB+countC+countD+countE+countF);
        printf("현재 전기공학과의 코로나 확진자: %d\n", countA);
        printf("현재 전자공학과의 코로나 확진자: %d\n", countB);
        printf("현재 정보통신공학부의 코로나 확진자: %d\n", countC);
        printf("현재 컴퓨터공학과의 코로나 확진자: %d\n", countD);
        printf("현재 소프트웨어학부의 코로나 확진자: %d\n", countE);
        printf("현재 지능로봇공학과의 코로나 확진자: %d\n", countF);
        
    }
    else
    {
        printf("데이터가 없습니다.\n");
    }
    
}
