## 智能蛇

智能蛇的大体框架和上篇博客提到的贪吃蛇没有太大的区别，在此就不复制粘贴那些代码了。 
要让贪吃蛇自己动起来的关键在于让蛇自己以一定的速度“走”起来。在这里我用了包含在#include < stdio.h >头文件下的sleep函数来控制这个过程。例如：
```
sleep(1000)
```
表示每执行到这一步时暂停1000毫秒。当然，我们也可以设定变化的速度，让智能蛇变成一条“变速蛇”。 
用如下的算法可以实现智能蛇的"自己动"。

```c
void AIMove() {
    int CanMove[4] = {1,1,1,1};
    if(map[AIsnake.y[0]][AIsnake.x[0]+1] != blank_char && map[AIsnake.y[0]][AIsnake.x[0]+1] != snake_food) CanMove[3] = 0;//right
    if(map[AIsnake.y[0]][AIsnake.x[0]-1] != blank_char && map[AIsnake.y[0]][AIsnake.x[0]-1] != snake_food) CanMove[1] = 0;//left
    if(map[AIsnake.y[0]-1][AIsnake.x[0]] != blank_char && map[AIsnake.y[0]-1][AIsnake.x[0]] != snake_food) CanMove[0] = 0;//up
    if(map[AIsnake.y[0]+1][AIsnake.x[0]] != blank_char && map[AIsnake.y[0]+1][AIsnake.x[0]] != snake_food) CanMove[2] = 0;//down

    if(food.x<=AIsnake.x[0] && food.y<AIsnake.y[0]) AIconstruct=0;
    if(food.x<AIsnake.x[0] && food.y>=AIsnake.y[0]) AIconstruct=1;
    if(food.x>=AIsnake.x[0] && food.y>AIsnake.y[0]) AIconstruct=2;
    if(food.x>AIsnake.x[0] && food.y<=AIsnake.y[0]) AIconstruct=3;

    while(!CanMove[AIconstruct]) AIconstruct = AIconstruct % 4 + 1;

    map[AIsnake.y[AIsnake.lenth-1]][AIsnake.x[AIsnake.lenth-1]] = blank_char;
    map[AIsnake.y[0]][AIsnake.x[0]] = AIsnake_body;
    int i = 0;
    for( i=AIsnake.lenth-1; i; i-- ) {
        AIsnake.x[i] = AIsnake.x[i-1];
        AIsnake.y[i] = AIsnake.y[i-1];
    } 
    switch(AIconstruct) {
        case 0: {AIsnake.y[0]--;
            break;
        }
        case 1: {AIsnake.x[0]--;
            break;
        }
        case 2: {AIsnake.y[0]++;
            break;
        }
        case 3: {AIsnake.x[0]++;
            break;
        }
    }
    if(map[AIsnake.y[0]][AIsnake.x[0]] != blank_char && map[AIsnake.y[0]][AIsnake.x[0]] != snake_food ) {
        GameWin();
    }
    if(map[AIsnake.y[0]][AIsnake.x[0]] == snake_food ) {
        map[AIsnake.y[0]][AIsnake.x[0]] = AIsnake_head;
        HaveFood = 0;
        AIsnake.lenth++;

    else map[AIsnake.y[0]][AIsnake.x[0]] = AIsnake_head;
```

以上就是进行优化后的”智能蛇“，但是有一点点bug。