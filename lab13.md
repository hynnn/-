## 任务1：会动的蛇

伪代码
```
输出字符矩阵
    WHILE not 游戏结束 DO
        ch＝等待输入
        CASE ch DO
        ‘A’:左前进一步，break 
        ‘D’:右前进一步，break    
        ‘W’:上前进一步，break    
        ‘S’:下前进一步，break    
        END CASE
        输出字符矩阵
    END WHILE
    输出 Game Over!!! 
```

```c
//先思考主函数体，再填充调用函数
#include <stdio.h>
#include <time.h>
#include <stdlib.h> 
#include <conio.h>
//声明常量
#define head 'H'
#define body 'X'
#define blank_char ' '

struct SNAKE    //用结构体定义蛇的位置和长度
{
    int x[100];
    int y[100];
    int lenth ;
}snake; 
//定义两个参数分别控制游戏的进程和方向
int gamerun = 1;     //1代表游戏继续，0代表游戏结束
char ch;             //蛇的方向
//采用字符型打印游戏界面
char map[10][11] = 
{
    "**********",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "**********" }; 
    
void PrintMap (){          //打印游戏界面的函数
    int i=0;
    system("cls");         //清屏
    for ( i=0; i<10; i++ ) {
        printf("%s\n", map[i]);
    }
}

void GameOver () {          //游戏结束的函数
    gamerun = 0;
    printf("GAME OVER!!!\n");
} 

void InitGame() {           //初始化整个游戏
    snake.y[0] = snake.y[1] = snake.y[2] = snake.y[3] = 1;
    snake.x[0] = 5;
    snake.x[1] = 4;
    snake.x[2] = 3;
    snake.x[3] = 2;
    snake.lenth = 4; 
    map[snake.y[0]][snake.x[0]] = head;
    map[snake.y[1]][snake.x[1]] = body;
    map[snake.y[2]][snake.x[2]] = body;
    map[snake.y[3]][snake.x[3]] = body;
    map[snake.y[4]][snake.x[4]] = body;
    gamerun = 1;
    PrintMap();
}

void MoveSnake (){          //蛇移动的函数
    int i = 0;
    scanf("%c",&ch);
//蛇改变方向时“头尾互换”的操作。
    map[snake.y[snake.lenth-1]][snake.x[snake.lenth-1]] = blank_char;

    map[snake.y[0]][snake.x[0]] = body;

    for( i=snake.lenth-1; i; i-- )
    {
        snake.x[i] = snake.x[i-1];
        snake.y[i] = snake.y[i-1];
    }  
    switch(ch)  //通过键盘上的小写‘w’，’a’，’s’，’d’控制蛇的移动
    {
        case 'w': snake.y[0]--; break;
        case 'a': snake.x[0]--; break;
        case 's': snake.y[0]++; break;
        case 'd': snake.x[0]++; break;
    }
    if(map[snake.y[0]][snake.x[0]] != blank_char )
        GameOver();
    else 
        map[snake.y[0]][snake.x[0]] = head;
}
//主函数体
int main() 
{
    InitGame() ;
    while (gamerun) 
    {   
        MoveSnake();
        PrintMap();
    }
    return 0;
}  
```

## 任务2：会吃的蛇

```c
//先思考主函数体，再填充调用函数
#include <stdio.h>
#include <time.h>
#include <stdlib.h> 
#include <conio.h>
//声明常量
#define head 'H'
#define body 'X'
#define blank_char ' '
#define food_char '$'

struct SNAKE    //用结构体定义蛇的位置和长度
{
    int x[100];
    int y[100];
    int lenth ;
}snake; 
struct FOOD     //食物位置
{
    int x;
    int y;
}food;

//定义两个参数分别控制游戏的进程和方向
int gamerun = 1;     //1代表游戏继续，0代表游戏结束
char ch;             //蛇的方向
//采用字符型打印游戏界面
char map[10][11] = 
{
    "**********",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "*        *",
    "**********" }; 
    
void PrintMap (){          //打印游戏界面的函数
    int i=0;
    system("cls");         //清屏
    for ( i=0; i<10; i++ ) {
        printf("%s\n", map[i]);
    }
}

void GameOver () {          //游戏结束的函数
    gamerun = 0;
    printf("GAME OVER!!!\n");
} 

void InitGame() {           //初始化整个游戏
    snake.y[0] = snake.y[1] = snake.y[2] = snake.y[3] = 1;
    snake.x[0] = 5;
    snake.x[1] = 4;
    snake.x[2] = 3;
    snake.x[3] = 2;
    snake.lenth = 4; 
    map[snake.y[0]][snake.x[0]] = head;
    map[snake.y[1]][snake.x[1]] = body;
    map[snake.y[2]][snake.x[2]] = body;
    map[snake.y[3]][snake.x[3]] = body;
    map[snake.y[4]][snake.x[4]] = body;
    gamerun = 1;
    PrintMap();
}

void MoveSnake (){          //蛇移动的函数
    int i = 0;
    scanf("%c",&ch);
//蛇改变方向时“头尾互换”的操作。
    map[snake.y[snake.lenth-1]][snake.x[snake.lenth-1]] = blank_char;

    map[snake.y[0]][snake.x[0]] = body;

    for( i=snake.lenth-1; i; i-- )
    {
        snake.x[i] = snake.x[i-1];
        snake.y[i] = snake.y[i-1];
    }  
    switch(ch)  //通过键盘上的小写‘w’，’a’，’s’，’d’控制蛇的移动
    {
        case 'w': snake.y[0]--; break;
        case 'a': snake.x[0]--; break;
        case 's': snake.y[0]++; break;
        case 'd': snake.x[0]++; break;
    }
    if(map[snake.y[0]][snake.x[0]] != blank_char && map[snake.y[0]][snake.x[0]] != food_char)
        GameOver();
    if(map[snake.y[0]][snake.x[0]] == food_char ) 
    {
        map[snake.y[0]][snake.x[0]] = head;
        snake.lenth++;    //遇上食物长度+1
        IsFood = 0;
    }
    else
        map[snake.y[0]][snake.x[0]] = head;
}

void SpawnFood ()     //食物随机出现
{
    food.x = rand() % 8 + 1;
    food.y = rand() % 9 + 1; 
    while(map[food.y][food.x] != blank_char) {
        food.x = rand() % 8 + 1;
        food.y = rand() % 9 + 1; 
    }
    map[food.y][food.x] = food_char;
    IsFood = 1;
}

//主函数体
int main() 
{
    InitGame() ;
    while (gamerun) 
    {
        srand(time(NULL));
        MoveSnake();

        if(!IsFood) 
            SpawnFood ();

        PrintMap();
    }
    return 0;
}  
```