# 字符游戏——贪吃蛇的设计思路

## 前言

贪吃蛇，一款极其经典的游戏。也是众多程序员入门的小程序。 但是贪吃蛇中却蕴含着大学问。如何让蛇自己动起来，能自己吃食物，并且还不能死亡以使蛇长度尽可能地长。这是一个很普通也很深奥的问题。

![](https://img-blog.csdn.net/20180103172409866?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvd2VpeGluXzM4MTkwNjUw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

## 设计思路

首先，我们用自顶向下的思路去考虑这个问题，先做一个可以在一定范围内通过键盘控制来移动的“蛇”。 

用伪代码来表示这个过程， 就是：
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

游戏结束的标志是贪吃蛇的头部撞到了“墙”。 
经过这样的分析，我们的游戏已经有了一定的框架。下面我们套用这个框架完成游戏的设计吧。

这是整个程序的头部,包括调用的库和使用的常量。
```
#include <stdio.h>
#include <time.h>
#include <stdlib.h> 
#include <conio.h>
//声明常量
#define head 'H'
#define body 'X'
#define blank_char ' '
```

游戏的对象“蛇”的属性包括位置和长度，用一个结构体来定义：

```
struct SNAKE    //用结构体定义蛇的位置和长度
{
    int x[100];
    int y[100];
    int lenth ;
}snake; 
```

定义两个参数分别控制游戏的进程和方向：

```
int gamerun = 1;     //1代表游戏继续，0代表游戏结束
char ch;             //蛇的方向
```

采用字符型式打印出游戏的界面：

```
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
```

接着我们就可以写函数主题部分了。

```
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

我们发现我们在函数主体中调用了自定义函数，那么我们接下来就要去填充函数。

**程设老师说过，先有用户需求调用函数，再去定义函数、补充函数。**


```
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
```

一条会动的蛇，就完成啦！ 

下面我们仅需要做一些简单的改动，就可以让它实现“会吃”的功能了。

首先，我们要添加食物定义

```
#define food_char '$'
```

接着，对象“食物”的属性是它的位置：

```
struct FOOD     //食物位置
{
    int x;
    int y;
}food;
```

我们还需要设置一个食物随机出现的函数：

```
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
```

由于蛇吃了食物会变长，所以我们还需要对void MoveSnake()这个函数进行一些修改，并对主函数体内添加函数void SpawnFood ()的调用即可。

## 总结

这里面出现了太多我未曾涉及的函数领域，第一次打，借鉴了前辈的经验，但是还是一堆bug,最大的收获就是“自上而下，逐步求精”的设计思路更加清晰。