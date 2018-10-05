# Construct 2:新手做游戏

## Construct 2
[Construct 2官网](https://www.scirra.com/construct2)
>Construct 2 is a powerful ground breaking HTML5 game creator designed specifically for 2D games. It allows anyone to build games — no coding required!

![](https://gss3.bdstatic.com/84oSdTum2Q5BphGlnYG/timg?wapp&quality=80&size=b150_150&subsize=20480&cut_x=0&cut_w=0&cut_y=0&cut_h=0&sec=1369815402&srctrace&di=ec7ffe97e4d5fee9a6e11b01d31155cc&wh_rate=null&src=http%3A%2F%2Fimgsrc.baidu.com%2Fforum%2Fpic%2Fitem%2F9f510fb30f2442a7ffa20912d043ad4bd01302dc.jpg)
## 制作第一个HTML5游戏

### 安装Construct 2
可参考官方[安装指南](https://www.scirra.com/manual/2/installing)

### 入门
启动Construct 2。单击File按钮，然后选择New。您将看到“模板或示例”对话框。
![](https://www.scirra.com/images/articles/newprojdialog65.png)

现在，在“新项目”对话框中你不需要改变任何选项，只需要点击“创造”项目便可。Construct 2将始终保持项目作为一个单一的.capx文件。而现在我们需要着眼于空白的布局——这是你所创造的设计视图以及目标位置。

### 插入对象
1. 背景
双击布局中的空白处以插入新对象(或者右击并选择" Insert new object"),弹出对话框后，双击“Tiled Background object ”将其插入。 
![]
(https://www.scirra.com/images/articles/insertobject.png)

将出现一个十字准线，指示放置对象的位置。单击布局中间附近的某个位置。编辑器会立即打开。导入您需要的图像。
单击右上角的X关闭纹理编辑器。如果系统提示您，请务必保存！现在，您应该在布局中看到平铺的背景对象。让我们调整它以覆盖整个布局。确保选中它，然后左侧的属性栏应显示对象的所有设置，包括其大小和位置。

![](https://www.scirra.com/images/articles/tiledproperties.png)

2. 添加图层
布局可以包含多个图层，您可以使用这些图层对对象进行分组。
要管理图层，请单击“Layers”选项卡，该选项卡通常位于“Project”栏旁边。
![]
(https://www.scirra.com/images/articles/layersbar.png)

您应该在列表中看到第0层,单击铅笔图标并将其重命名为Background，因为它是我们的背景图层。现在单击绿色的“添加”图标为我们的其他对象添加新图层。我们称之为一个Main。最后，如果单击“ 背景”旁边的小挂锁图标，它将被锁定。这意味着您将无法选择它。

3. 添加输入对象

将注意力转回布局。双击以插入另一个新对象。这次，选择Mouse对象，因为我们需要鼠标输入。对Keyboard对象再次执行相同操作。

4. 添加游戏对象

此时您可以添加游戏所需的对象，对于每个对象，我们将使用精灵对象。它只显示一个纹理，您可以移动，旋转和调整大小。游戏通常主要由精灵对象组成。

该过程类似于插入平铺背景：
* 双击以插入新对象
* 双击 “Sprite”对象。
* 当鼠标变为十字准线时，单击布局中的某个位置。
* 弹出纹理编辑器。
* 关闭纹理编辑器，保存更改。

### 添加行为

行为是Construct 2中的预打包功能。其中，Construct 2有这些行为：
- 8方向运动。这使您可以使用箭头键移动对象。它会很好地适应玩家的运动。
- 子弹运动。这只是以当前角度向前移动一个物体。它对玩家的子弹很有用。尽管有这个名字，它也可以很好地移动怪物 - 因为所有的移动都是以某种速度向前移动物体。
- 滚动到。这使得屏幕在移动时跟随对象（也称为滚动）。这对玩家有用。
- 绑定到布局。这将停止一个物体离开布局区域。这对玩家也很有用，所以他们不能在游戏区域外游荡！
- 破坏外部布局。而不是停止离开布局区域的对象，如果它停止，则会破坏它。它对我们的子弹很有用。没有它，子弹将永远飞离屏幕，总是占用一点内存和处理能力。相反，我们应该在他们离开布局后销毁子弹。
- 淡出。这逐渐使物体淡出，我们将用于爆炸。

如何添加行为

例如添加8方向移动行为。单击播放器以选择它。在属性栏中，请注意“Behaviors ”类别。单击“Add / Edit”。播放器的“ Behaviors ”对话框将打开。

![](https://www.scirra.com/images/articles/openbehaviors.png)

单击行为对话框中的绿色图标。双击8方向移动以添加它。

![](https://www.scirra.com/images/articles/add8dir.png)

### 活动

首先，单击顶部的“ 事件表1”选项卡以切换到“ 事件”表编辑器。事件列表称为事件表，您可以为游戏的不同部分或组织设置不同的事件表。

关于活动

正如空白工作表中的文字所示，Construct 2每个tick都会在事件表中运行一次。大多数显示器每秒更新其显示器60次，因此Construct 2将尝试匹配最平滑的显示器。这意味着事件表通常每秒运行60次，每次都重新绘制屏幕。这就是刻度线 - 一个单元“运行事件然后绘制屏幕”。

条件，行动和子事件

事件由条件组成，测试是否满足某些条件，例如“空格键是否已关闭？”。如果满足所有这些条件，则事件的所有操作都会运行，例如“创建项目符号对象”。运行后，任何子事件也会运行 - 然后可以测试更多条件，然后运行更多操作，然后运行更多子事件，等等。使用此系统，我们可以为我们的游戏和应用程序构建复杂的功能。

如何添加活动

我们以让对象总是看着鼠标为例。
让我们开始制作这个活动。双击事件表中的空格。这将提示我们为新事件添加条件。

![](https://www.scirra.com/images/articles/newevent_2.png)

不同的对象具有不同的条件和动作，这取决于它们可以做什么。还有System对象，它表示Construct 2的内置功能。双击 System对象，如图所示。然后，该对话框将列出所有System对象的条件：
![](https://www.scirra.com/images/articles/everytickcnd.png)

双击的每个标记的条件，将其插入。对话框将关闭并创建事件，不执行任何操作。它现在应该是这样的：

![](https://www.scirra.com/images/articles/everytickempty.png)

现在我们要添加一个动作让对象看鼠标。单击事件右侧的“ 添加操作”链接。（确保您获得添加操作链接，而不是其下方的添加事件链接，这将再次添加完整的不同事件。）将出现“添加操作”对话框：

![](https://www.scirra.com/images/articles/addactiondlg.png)

与添加事件一样，我们有相同的对象列表可供选择，但这次是添加操作。尽量不要在添加条件和添加操作之间感到困惑！如图所示，双击该播放器的对象，因为这是我们要看看鼠标的对象。将显示Player对象中可用的操作列表：

![](https://www.scirra.com/images/articles/playersetanglepos.png)

我们想要将角度设置为鼠标位置。Mouse对象可以提供此功能。输入Mouse.X为X，和Mouse.Y为ÿ。这些被称为表达式。
最后，动作被添加，如图：

![](https://www.scirra.com/images/articles/alwayslookatmouse.png)

### 添加游戏功能

如果每个事件都像以前一样详细描述，那么这将是一个相当长的教程。让我们为下一个事件做一些简短的描述。请记住，添加条件或操作的步骤如下：

1. 双击以插入新事件，或单击“ 添加操作”链接以添加操作。
2. 双击条件/操作所在的对象
3. 双击所需的条件/操作。
4. 输入参数（如果需要）。

### 实例变量

变量只是一个可以改变（或变化）的值，它们是为每个实例单独存储的，因此是名称实例变量。单击项目栏或对象栏中的对象。或者，您可以切换回布局并选择对象。这将在属性栏中显示对象的属性。点击添加/编辑通过编辑变量。

## 最后

 Construct 2 功能强大，笔者不能全部写下所有功能，详细可以看官网论坛，鼓励大家制作自己的游戏。

下面是我第一个HTML5游戏展示

 ![](images\1111.gif)










