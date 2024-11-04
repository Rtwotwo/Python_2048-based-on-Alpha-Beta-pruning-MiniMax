<<<<<<< HEAD
# Python_2048-based-on-Alpha-Beta-pruning-MiniMax
This program mainly designs the player mode and AI mode of Python 2048. The AI mode mainly uses the Alpha-Beta pruning algorithm to implement the 2048 game, bringing users a different gaming experience.

=======
# Python 2048 Game

本项目实现了基于 Alpha-Beta 剪枝的 Minimax 算法的 Python 2048 游戏。

## 功能介绍

该项目的主要功能包括：

1. **基本游戏规则**：
   - 玩家通过方向键移动数字方块，使相同数字的方块合并，每次合并后获得得分。
   - 当出现 `2048` 数字时游戏胜利。
   - 每次移动后，会在空白区域随机产生 `2` 或 `4`。
   - 若方格被填满则游戏结束。

2. **游戏模式**：
   - **正常模式**：玩家自行控制游戏。
   - **提示模式**：显示推荐的移动方向，帮助玩家更好地进行游戏。
   - **人工智能模式**：游戏自动进行，使用 Alpha-Beta 剪枝的 Minimax 算法实现智能决策。

3. **增强功能**：
   - **美观性增强**：为不同的数字添加了背景色，优化了积分显示界面。
   - **音效控制**：添加了游戏背景音乐，并且背景音乐进行随机的循环播放设置，同时增添了游戏音效的开关控制。
   - **动态效果**：为游戏的滑块添加了移动动态效果。

## 截图

![2048游戏界面显示](game_interface.png)

## 技术栈

- **Python 版本**：3.x
- **依赖库**：
  | 序号 | 库名称      | 版本     | 简介                                         |
  |------|-------------|----------|----------------------------------------------|
  | 1    | os          | 3.12.2   | 操作系统接口，用于文件和目录操作             |
  | 2    | numpy       | 1.26.4   | 高性能数值计算库，支持数组运算               |
  | 3    | copy        | 3.12.2   | 深拷贝和浅拷贝对象                           |
  | 4    | random      | 3.12.2   | 生成伪随机数                                 |
  | 5    | time        | 3.12.2   | 时间相关功能，如延时和计时                   |
  | 6    | pygame      | 2.5.2    | 游戏开发库，支持图形和声音                   |
  | 7    | sys         | 3.12.2   | 访问 Python 解释器的变量和函数               |
  | 8    | math        | 3.12.2   | 数学函数，如三角函数和对数                   |

## 开发环境

- **操作系统**：Windows 10/11, MacOS 14/15, Linux 系列
- **开发工具**：PyCharm

## 安装与运行

1. **安装依赖库**：

   ```bash
   pip install numpy pygame
>>>>>>> 0a2b5b820ba0f7b3cdc914f35894778033774cc1
