                           
 
目  录

1. 设计概述	1
1.1 设计目的	1
1.2 设计内容	1
1.3 应用平台	2
1.4 开发工具	2
1.5 软件库	3
1.6 测试数据	3
2. 详细设计	3
2.1 总体方案	3
2.2功能实现	9
2.2.1 2048基本游戏功能实现	9
2.2.2 游戏界面功能实现	10
2.2.3 游戏智能模式功能实现	12
2.2.4 游戏main()模式切换功能实现	17
3. 完成情况	17
3.1 程序运行结果	17
3.2 程序使用说明	19
3.3 主要研究过程	20
4. 设计总结	21
4.1 成员分工	21
4.2 存在的问题	21
4.3 改进的措施	21
4.4 课程的收获	22
4.5 对课程的建议	22
5. 附录	23
5.1 程序源码	23
5.2 其他	23





 
1. 设计概述
1.1 设计目的
本课程——智能人机交互与视觉感知综合设计，需要具备扎实的python代码能力要求、应对工程创新的能力、软件系统设计的全局协同能力。因此，本课程要求设计python2048小游戏，涵盖的目的：（1）、通过从零实现python2048的过程中，不断提高对python函数、列表、字典以及类的运用熟练程度；（2）、在设计过程中，学会合理地构建系统，分析代码调试以及测试功能等综合技巧；（3）、提升查找文献以及综合设计地能力，python2048的智能功能不仅仅要求会编程，还需要对常用的算法有一定的了解，不断提高遇到算法设计难题的应对能力。（4）、进一步理解人机交互与智能系统的本质与设计实现，为课程后续的学习内容打下坚实的基础。
1.2 设计内容
本课程通过要求设计实现python2048小游戏的相关基础功能：（1）、基本游戏规则：简单的移动方向键让数字叠加，并且获得这些数字每次叠加后的得分，当出现 2048 这个数字时游戏胜利；（2）、每次移动方向键时，都会在4*4的方格矩阵的空白区域随机产生2或4，若方格被填满则游戏结束；（3）、实现三种基本的游戏模式：正常模式，提示模式和人工智能模式。
为增添游戏乐趣以及可视美观化：（1）、从2至2048不同种类的数字添加了背景色；（2）、优化了积分显示界面；（3）、在提示模式下，完成了游戏提示的界面显示；（4）、添加了游戏背景音乐，并且背景音乐进行随机的循环播放设置，同时增添了游戏音效的开关控制；（5）、优化了游戏界面的字体显示，提高2048的游戏程序界面的观感。参考基于Alpha-Beta剪枝的Minimax的Minimax的算法原理分别设计了一套完整的python 2048游戏，如下面的游戏界面显示。并且，结合各方优势，提升了2048智能模式的可靠性。同时，为游戏添加了背景音效开关控制；刘宇轩为游戏的滑块添加了移动动态效果；并且设计的游戏均能够通过键盘点击或者鼠标点击来实现移动滑块或者完成相关功能。
 	 
图1 2048游戏界面显示
1.3 应用平台
Windows 10/11及其家庭版; 
MacOS 14/15; Linux系列
1.4 开发工具
开发工具使用Pycharm

1.5 软件库
表1 使用的Python库和版本
序号	库名称	版本	简介
1	os	3.12.2	操作系统接口，用于文件和目录操作
2	numpy	1.26.4	高性能数值计算库，支持数组运算
3	copy	3.12.2	深拷贝和浅拷贝对象
4	random	3.12.2	生成伪随机数
5	time	3.12.2	时间相关功能，如延时和计时
6	pygame	2.5.2	游戏开发库，支持图形和声音
7	sys	3.12.2	访问 Python 解释器的变量和函数
8	math	3.12.2	数学函数，如三角函数和对数
1.6 测试数据
游戏界面开发过程中，使用到了游戏背景音乐、字体数据、游戏方块RGB色数据，作为提高游戏体验感以及游戏界面的美观性的辅助开发。相关数据的名称、来源、数量信息、用途如下表所示：
表2 测试数据的相关信息
	来源	数量信息	用途
背景音乐	https://www.aigei.com/	14	用于2048背景音乐
字体	https://www.58pic.com/	1	用于游戏界面
字体显示
方块RGB色	https://www.rapidtables.org/zh-CN/web/color/RGB_Color.html	12	用于绘制美观的2048游戏棋盘
2. 详细设计
2.1 总体方案
本组成员均是基于Alpha-Beta剪枝的MiniMax原理，而具体的Alpha-Beta剪枝MiniMax算法见后续原理讲解所示。本组两组员各自设计一套python2048程序，相关的程序总体设计方案：以类的方式定义棋盘状态、AI智能模式、pygame界面显示三个主要常用类，最后在主程序的main()定义以及调用各类中的函数。具体代码的程序结构，各函数功能关系，参数传递等信息如下所示。
 
图2 程序代码的整体框架示意图
GameState类下的各个函数负责处理棋盘移动、滑块合并、得分计算等功能的实现。调用GameState类的流程是：首先初始化GameState类实例时，传入游戏板状态；然后使用move函数根据指定的方向移动游戏板上的瓷砖；紧接着使用is_game_over函数检查游戏是否结束；使用insert_tile函数在空闲位置随机插入新的瓷砖，使用find_max_index函数寻找最大数值的位置，最后使用 Is_game_succeed 函数判断游戏是否胜利。当然，GameState类中也设置了例如玩家状态self.play_turn、游戏得分self.score、预测方向self.dir属性。
表3 GameState类函数功能宇参数传递表
	函数功能	参数传递
__init__	初始化GameState实例
参数board（默认为 None）：一个 4x4 的二维数组，代表游戏板的状态。如果未提供，则创建一个全零数组	接收一个可选参数 board，
用于初始化游戏状态
find_max_index	寻找游戏板上最大数值的位置	直接使用实例变量self.game_state
Is_game_succeed	检查游戏板上是否存在 2048的数值，以此判断游戏是否胜利	直接使用实例变量self.game_state
move	根据指定的方向（左、上、右、下）移动游戏板上的瓷砖；参数 direction：整数，表示移动方向，返回True如果发生了移动，否则返回False	接收一个整数参数 direction，表示移动方向
_merge_left	辅助函数，用于处理向左移动时的合并逻辑;参数non_zero一维数组，包含非零元素;返回合并后的数组和合并产生的分数	直接使用实例变量self.game_state
insert_tile	在指定位置插入一个瓷砖:
表示位置的整数坐标；参数 value:要插入的瓷砖的数值,返回True如果成功否则返回False	接收两个整数参数x和y及一个整数参数 value，用于插入瓷砖
remove_tile	删除指定位置的瓷砖
参数x和y：表示位置整数坐标	接收两个整数参数 x 和 y，
用于删除瓷砖
get_available_cells	返回一个列表，包含所有空闲格子的位置	直接使用实例变量self.game_state
can_merge	检查游戏板上是否存在可以合并的相邻瓷砖	直接使用实例变量self.game_state
is_game_over	检查游戏是否结束
如果存在空闲格子或可以合并的瓷砖，则游戏没有结束；否则游戏结束	直接使用实例变量self.game_state
undo_move	用于测试移动后恢复游戏状态	接收一个整数参数 direction，用于撤销移动
__str__	返回游戏板的字符串表示形式	直接使用实例变量self.game_state
 
图3 GameState类的各函数功能关系示意图
AI类函数调用的总体流程：初始化AI类实例时，传入由GameState类创建的游戏状态对象，紧接着使用evaluate函数评估当前游戏状态，然后在需要做出决策时，调用iterative_deepening_search函数，传入超时时间参数，得到最佳移动方向，最后使用得到的最佳移动方向进行游戏。
表4 AI类函数功能宇参数传递表
	函数功能	参数传递
evaluate	计算当前游戏状态的总评价分数，包括平滑性、
单调性、空闲格子数量的对数和最大值的对数	直接使用实例变量self.game_state
smoothness	计算游戏板的平滑性，即数值
相近的格子之间的距离之和	使用 self.game_state
来获取游戏板的状态
monotonicity	计算游戏板的单调性，即每行和每
列的数值按顺序递增或递减的程度	使用 self.game_state
来获取游戏板的状态
search	使用 MiniMax 算法进行深度优先搜索；
接受参数depth（搜索深度）、alpha和beta（剪枝阈值）、positions（搜索位置计数）cutoffs（剪枝计数）；
返回一个字典，包含最佳移动方向、得分、搜索位置计数和剪枝计数	接受搜索深度、Alpha-Beta 剪枝阈值、搜索位置计数和剪枝计数作为参数，并返回最佳移动方向、得分、搜索位置计数和剪枝计数
iterative_deepening_search	使用迭代加深搜索算法，在给定的时间限制内尽可能深地搜索游戏树；接受一个参数 timeout_ms，表示搜索的超时时间（毫秒）；返回最佳移动方向	接受一个人为设定的超时时间作为参数，并返回最佳移动方向
islands	计算游戏板上“岛屿”的数量，即不
相连的相同数值格子群的数量	使用 self.game_state
来计算“岛屿”数量
_mark	辅助函数，用于标记与某个格子相同的邻居格子	接收一个 game_state 对象，标记与某个格子相同的邻居格子
 	
图4 AI类的各函数功能关系示意图	
调用Show类的基本流程是:初始化由GameState创建的对象的Show类实例，传入游戏状态对象；然后使用game_board函数绘制游戏界面；随后当需要时，调用music_on_off函数来控制背景音乐的播放；游戏结束时，根据游戏状态调用show_game_lost或 show_game_succeed函数来显示相应的消息。
当然也涉及Show类的实现细节：（1）色彩管理：使用字典color_bar 来存储不同的数字对应的背景颜色；（2）界面布局：使用 Pygame 的绘图函数来绘制界面元素，如矩形、文本等；（3）音乐播放：从指定的目录中随机选择背景音乐文件并使用 Pygame 的音频模块播放。
表5 Show类函数功能宇参数传递表
	函数功能	参数传递
__init__	函数初始化显示相关配置和数据	接收一个game_state对象，该对象应该包含游戏当前的状态信息，如游戏板状态、玩家得分等
game_board	函数负责绘制整个游戏界面，包括棋盘、得分、帮助提示等	使用 self.game_state 和其他实例变量来绘制游戏界面
music_on_off	函数控制背景音乐的播放或暂停	无需额外参数，直接使用 self.music_control 控制音乐的开关
show_game_lost	函数分别在游戏失败时显示相应的消息	无需额外参数，直接在屏幕上显示消息
show_game_succeed	函数分别在游戏胜利时显示相应的消息	无需额外参数，直接在屏幕上显示消息
2.2功能实现
2.2.1 2048基本游戏功能实现
（1）、棋盘上、下、左、右四个方向的移动原理：首先针对一维的列表来说，含有四个数字元素的列表，将其向左移动需要清除数字之间为0的元素，并且实现同类方块可以合并的效果。因此，我们首先创建一个_merge_left函数专门处理非零一维列表元素合并的问题，需要以每一行为处理单元，将棋盘的每一行中不含0的元素按顺序提取出来作为一组新的列表，将其传入到_merge_left中得到合并之后的非0列表。返回的列表，我们通过len计算新列表的长度，若是小于4，则在新列表后面增加4-len(merged_list)个0元素，以对齐4个格子。从而完成了向左移动并合并同类元素的要求。而上、下、右三个方向不变，通过转置处理来实现，例如上则先转置为左，移动合并处理后，再转置回来即可。
（2）、游戏胜利、失败功能检测原理：首先我们定义一个检测棋盘最大数字的函数find_max()，使用numpy数组的np.max()的嵌套获取到最大数，若最大数大于等于2048即游戏胜利。

而游戏失败则需要满足两个条件：棋盘没有空格并且相邻俩个数字无法合并。首先，定义全局变量Flag为True代表游戏已经失败，然后我们定义查询棋盘是否含有空格的函数，是则返回False。若返回True,则利用双层for循环从棋盘左上角（0，0）的位置开始遍历列表每一个元素，检测该元素的右侧和下侧是否与该元素相同。若存在相同，则将Flag置为False代表游戏还未失败。
（3）、游戏得分统计的实现：
在游戏程序中的GameState类中，我们定义一个self.score属性，在游戏的移动合并同类方块的函数中，当一行的列表相邻两个方块可以合并，我们就将其合并后的结果作为一个分类进行累加，最后传递给self.score进行统计即得到总得分。
2.2.2 游戏界面功能实现
 	 
图5 游戏16格棋盘和功能界面显示
（1）、游戏16格棋盘显示原理：2048游戏界面显示函数需要用到pygame.draw.rect函数来绘制方块。首先，我们在Show类中定义一个screen属性，用于后续在其上绘制相关的图案。紧接着，定义了一个color_bar字典包含了从2至2048的游戏可能出现的数字作为键，而对应的RGB三色元组作为值。随后利用嵌套for循环来实现。两层for循环分别定义的row和col分别作为每一个方格的左上角的坐标，如pygame.draw.rect(self.screen, self.color_bar[self.game_state.board[row][col]],[100+100*row,150+100 * col,95,95],0,10)这样的形式。随后，利用调研找到的字体联想小新潮酷体来定义一个self.font属性，同样利用双层for循环在每个方块上进行字体渲染，需要用pygame.font.Fon()函数、self.font.render()以及self.screen.blit()函数进行渲染。
（2）、功能界面显示以及功能切换原理：
首先功能界面如图5所示，一共有3行，我们需要一行一行的进行处理。将每一行所要显示的字体分别存入到列表中，再利用双层for循环来实现字体显示，不过我们使用enumerate函数来提取列表中的字体，对应的序号作为循环变量来绘制方块，即可完成。
同时，在main()函数中，我们明确定义好音乐-开/关、智能-开/关、重开-点击的界面坐标范围，然后在main()函数的while循环中，我们使用pygame.mouse.get_pos()函数来确定鼠标是否落入相应的范围中，在进一步判断鼠标是否在此区域进行了点击，若点击，则调用Show类来切换类中的属性值，从而实现对音乐、智能模式和游戏重新开始的控制。
（3）游戏胜利或失败显示原理：参考上述字体显示的原理。我们重新在Show类的胜利和失败的函数定义字体，将字体调大，并且放弃字体的背景色再进行显示。在main()主函数中，程序每一次循环均调用GameState类中的游戏胜利或失败函数作为if条件进行判断，若成立，则结束游戏显示相应字体。
 	 
图6 游戏胜利和失败的字体显示
2.2.3 游戏智能模式功能实现
（1）、基于Alpha-Beta剪枝的MiniMax算法原理：a.Minimax算法的步骤实现是首先确定最大搜索深度D，D可能达到终局，也可能是一个中间格局；b.在最大深度为D的格局树叶子节点上，使用预定义的价值评价函数对叶子节点价值进行评价；c.自底向上为非叶子节点赋值，其中max节点取子节点最大值，min节点取子节点最小值；d.每次轮到我方时（此时必处在格局树的某个max节点），选择价值等于此max节点价值的那个子节点路径。
 
图7 MiniMax算法示意（正方形-玩家移动；三角形-电脑移动）
由此，我们借用同样的思想，当前我们需要定义一个评价函数evaluate函数，用于对当前棋盘各方块数字分布进行打分。然后，确定最大搜索深度之后，将棋盘在四个方向进行模拟移动，然后使用综合评价函数对四个方向得到的子节点棋盘进行打分，临时记录四个方向的得分数据，再对移动后的子节点棋盘进行模拟移动，循环往复，不断迭代直到规定的迭代深度。
但是，需要考虑的是，由于如果每个子节点都向四个方向进行推理，程序的运行时间会过长，并且对于某些方向的移动其结果本身可能会导致棋盘的整体评价得分降低，从而导致游戏失败。因此，我们需要针对某些节点进行删减——即剪枝。我们引入Alpha-beta剪枝是对Minimax的补充和改进，采用Alpha-beta剪枝后，我们可不必构造和搜索最大深度D内的所有节点。
 
图8 基于Alpha-Beta的MiniMax算法示意（正方形-玩家移动；三角形-电脑移动）
其算法原理如图8所示具体是：在搜索过程中，算法维护两个边界值：alpha和beta，其中alpha代表当前搜索路径已知的最好选择的下限，而beta代表对手可能采取的最佳反击策略的上限。每当搜索到某个节点时，如果发现当前节点的beta值小于或等于其父节点的alpha值，这意味着从当前节点开始的搜索路径无论如何选择都不会优于已知的最佳路径，因此可以提前终止这条路径的搜索，即进行剪枝。通过这种方式，Alpha-Beta剪枝有效地减少了搜索空间，提高了搜索效率，使得算法能够在相同时间内探索更深的搜索树，进而找到更优的解决方案。
（2）、迭代深度搜索函数的实现原理：在AI类中的search函数，我们首先定义alpha为负无穷大——代表玩家当前棋盘的状态，beta为正无穷大——代表电脑移动的状态。随后，我们依据GameState类中的移动的角色判断self.play_turn来判断是玩家还是电脑在移动棋盘。在search函数的if-else语句中：1、if代表模拟玩家的移动，遍历所有可能的方向，对于每个方向，创建一个新的游戏状态副本，并尝试移动。比较alpha与beta的值，如果alpha大于beta则代表移动成功，则递归调用 search 函数进入下一深度并更新alpha和beta的值，同时进行剪枝；2、else语句代表电脑模拟移动，遍历所有可能插入新方块的位置。评估每个位置插入新方块后的得分。选择最佳位置插入新方块，检查游戏是否结束，如果是，则尝试所有方向并选择导致合并的方向。如果没有有效的移动，则返回默认值。
而在iterative_deepening_search()函数中，为保证找到最合适的深度搜索深度与搜索时长，我们使用time函数来计时搜索的实践并将其与人为设定的阈值比较作为while函数的条件。每一次循环，迭代深度逐渐增加，直到返回最佳移动方向best_move,从而达到深度搜索的效果。
(3)、评价函数的实现原理：评价函数主要涉及到棋盘平滑性、单调性、空格数、最大值四个评价因素的综合影响。而且空格数empty_cells、max_value可有GameState类中的get_available_cells()和find_max_index()函数来获取。我们需要定义平滑性smoothness()和单调性monotonicity()函数。对于平滑性smoothness()，我们选择使用双层for循环遍历棋盘的每一个元素，并计算该元素对应得log2(x)的值，随后再次统计该元素相邻得上下左右四个元素的log2(x)值，根据光滑性smoothness计算公式（1）统计出该棋盘光滑性总和。
 
（1）
 
图9 棋盘光滑性Smoothness2048示例
对于单调性monotonicity()，使用双层for循环遍历棋盘的每一行和每一列，对于每一行和每一列，它跳过空格子，并利用对数函数计算相邻非空格子之间的递增或递减趋势。通过比较当前格子和下一个格子的对数值，如果当前格子的值大于下一个格子的值，则增加递减趋势的总和；如果当前格子的值小于下一个格子的值，则增加递增趋势的总和。最终，函数返回最大递增趋势和最大递减趋势之和，以此来反映棋盘布局的单调性。这一实现利用了NumPy数组作为数据结构来存储棋盘状态，并通过逐行逐列的遍历来评估棋盘的单调性，从而帮助AI更好地评估游戏局面。
 
（2）
 
（3）
 
图10 棋盘单调性monotonicity2048示例
2.2.4 游戏main()模式切换功能实现
定义main()函数，其内游戏主循环包括鼠标位置检测（配合音乐控制、模式切换）、AI模式切换、玩家模式。Main()函数首先初始化棋盘、定义好特定的鼠标区域包括音乐开关、模式切换和游戏重开三个方块区域。随后进入游戏主循环，循环内首先进行使用pygame.event.get()来检测电脑当前状态：a.使用if条件判断游戏是否需要退出，若成立使用pygame.quit()退出；b.使用pygame.mouse.get_pos()来定义区域，然后使用定义好的区域collidepoint()来判断是否在相应区域点击；c.若在音乐或智能区域点击，则调用Show类的属性self.music_control或者self.ai_control来翻转开-关状态；d.随后的程序中，再使用if-else分别包含AI模式和玩家模式并使用self.ai_control来作为条件控制。
游戏状态重开，则是通过mouse.get_pos()来实现，若在“点击”区域发生点击事件，则将main()的GameState的游戏棋盘进行重新初始化,将棋盘清空并随机放置一个2即可。在游戏结束之后，会嵌套调用main()实现游戏重新开始。倘若，main()函数结束之后，则会立即调用self.score将其存储在history_score.txt文件中。
3. 完成情况
3.1 程序运行结果
本次python2048小游戏的设计，基于Alpha-Beta剪枝的MiniMax算法完成了对棋盘的深度搜索，通过模拟推理基本完成了正常模式，提示模式和人工智能模式的游戏切换综合设计。
相应的本组两组员分别设计的程序运行过程图和结果图如图11所示：
 	 
 	 
图11 两个程序运行的结果展示
程序运行过程中的截图，上面两组图片是Rtwotwo设计的2048小游戏程序，左图是游戏运行过程中的截图，右图是游戏运行结果的截图；下面两组图片是刘宇轩设计的2048小游戏程序，左图是游戏运行过程中的截图，右图是游戏运行结果的截图。
3.2 程序使用说明
1、Rtwotwo设计的2048：
a.	运行时，音乐和智能默认为“关”，棋盘处于玩家手动控制的状态；
b.	玩家模式下，可以通过键盘上的“上、下、左、右”或“w、s、a、d”来进行控制合并同类方块；
c.	在游戏过程中，可以点击“音乐”后的“开/关”实现游戏音乐的控制，可以反复点击“开/关”来随机切换不同的音乐，系统存储14首音乐；
d.	在游戏过程中，可以点击“智能”后的“开/关”实现玩家模式和智能AI模式的切换，智能AI模式可以自主运行直到游戏结束；
e.	游戏运行中，或是游戏结束（胜利/失败）时，均可以通过“重开”后的“点击”，来刷新游戏棋盘，重新开始游戏；
f.	游戏界面的下面“最高分”表示从系统更新开始每一次运行的分数的最高分，游戏结束不会影响此分数的变化。
2、LYX设计的2048：
a. 运行时，第一行“Score”表示当局的分数，“Highest”表示游戏运行开始的到当前的最高分，中间表示整个棋盘；
b. 游戏时，可以点击“帮助模式”会弹出“游戏提示：方向”的提示指令；
c. 可以点击“智慧核心”来实现游戏的自主运行，直到游戏结束；
d. 点击下方的“重新开始”,清空游戏棋盘重新开始游戏；
e. 游戏进行过程中，可以通过键盘上的“上、下、左、右”来进行控制合并同类方块,并且游戏方块在移动过程中有移动效果。

3.3 主要研究过程
表5 游戏2048设计开发流程日记（以刘宇轩开发为例）
初步设计与架构	本组成员经过讨论之后，确定游戏的初步实现实现方法，决定分别设计实现2048游戏，经过查找资料之后，决定采用Alpha-Beta剪枝MiniMax算法来实现智能AI模式。同时，我们确定设计的游戏需要有pygame的游戏界面。
实现基本游戏逻辑	主要工作是完善游戏的基本逻辑：我们分别添加了OperateUp、OperateDown、OperateLeft和OperateRight等相似的方法来处理不同方向的移动逻辑。同时，我还实现了Summon方法来随机生成新的数字（通常是2或4），并确保游戏的进行。为了方便测试，我还添加了initial方法来初始化游戏界面。
游戏界面与动画效果	专注于实现游戏的界面和动画效果：使用pygame库来绘制游戏界面，包括棋盘背景、按钮和游戏文字提示。我还实现了show方法来显示当前棋盘状态，并添加了MoveAnimation和NewAnimation方法来模拟数字移动和新数字生成的动画效果。为了让游戏更加生动，我还添加了draw_lines方法来绘制棋盘的线条。
游戏结束与帮助模式	工作重点是处理游戏结束的情况以及实现帮助模式：实现了over方法来检测游戏是否结束，以及drawover方法来展示游戏结束的画面。此外，还添加了drawhelp方法来显示推荐的移动方向，以帮助玩家更好地进行游戏。
人工智能与自动模式	开始设计游戏的人工智能部分：创建一个AI类，用于实现自动模式下的游戏决策。首先，实现了get_next方法来获取下一步的最佳移动方向。还添加了get_tile_num和get_score方法来辅助计算棋盘状态的评估分数。为了模拟多步预测，还实现了get_grid方法来获取指定移动序列后的棋盘。
优化与调试	今天主要进行了程序的优化和调试：注意到游戏的自动模式有时会选择不太理想的方向，因此我对get_next方法进行了调整，使其更加智能。本组成员分别优化自己的OperateUp等移动方法，确保它们能够正确处理各种边界条件。最后，我还进行了一系列的测试，确保游戏在各种情况下都能正常运行。
最后，保证游戏的代码提高自主运行到2048的概率，同时处理程序运行遇到的各种的问题。

4. 设计总结
4.1 成员分工
成员一：Rtwotwo		2022302039		08062203			电子信息学院
主要完成：小组2048游戏报告，2048游戏的基础移动合并操作、2048界面显示、游戏背景音乐开关控制以及随机播放、玩家/AI模式切换、Alpha-Beta剪枝MiniMax算法实现深度搜索AI、游戏重启功能、游戏胜利/失败界面显示；
成员二：LYX		2022302045		08062203			电子信息学院
主要完成：2048游戏的基础移动合并操作、2048界面显示、2048游戏移动效果显示、玩家/AI模式切换、Alpha-Beta剪枝MiniMax算法实现深度搜索AI、游戏重启功能、游戏胜利/失败界面显示。
4.2 存在的问题
1、游戏目前需要将小组成员的两个程序的进行结合，优化程序的综合性能；
2、对于Rtwotwo的程序，需要调节MiniMax算法的评价函数的参数，提高游戏AI模式进行深度搜索的运行速度和效果；
3、对于LYX的程序，例如界面游戏失败检测并显示的功能有问题，当游戏运行至2048之后，游戏并没有结束。当游戏结束之后，重新开始游戏，程序可能会卡住。
4.3 改进的措施
小组计划将程序规范化，按照类的方法将各个功能函数进行打包处理，结合小组双方的程序的优缺点，升级AI模式的性能，优化游戏界面的显示，提高游戏的美观效果。

4.4 课程的收获
成员一：在团队合作方面，我也积累了宝贵的经验。与队友一起解决问题、分配任务和共同完成项目的过程中，我提高了沟通技巧和协作能力。特别是在遇到难题时，团队合作的力量尤为重要。通过阅读和理解他人的代码，我的代码解读能力和调试技巧也有了显著提升。这些经验将对我未来的学习和职业发展产生积极影响。这门课程不仅增强了我的技术能力，也培养了我的团队合作精神和解决问题的能力，为我将来从事相关领域的工作打下了坚实的基础。
成员二：通过本次课程的学习和实践，我获得了多方面的收获。首先，我深入了解了游戏AI的设计与实现，特别是像2048这样的策略游戏。通过对Minimax算法以及Alpha-Beta剪枝的理解与应用，我学会了如何构建有效的决策树，并利用剪枝技术来提高算法的效率。这些技术不仅适用于2048游戏，还可以应用于其他类似的策略游戏开发中。
我掌握了使用Python进行游戏开发的基础知识，包括如何使用Pygame库来构建游戏界面，并实现了游戏的基本逻辑。此外，我也学习了如何运用numpy和其他库来处理游戏中的数学运算和数据结构操作。
4.5 对课程的建议
成员一：课程设计上，建议增加一些案例分析和实际应用场景的讲解，让学生了解所学知识在现实世界中的应用，这样可以激发学生的学习兴趣；讲授方式上、希望老师能够提供更多的参考资料和学习资源，比如在线教程和书籍推荐，这样可以帮助学生在课外自主学习。
成员二：评估方式上，建议增加一些开放性的问题和项目，这样可以鼓励学生发挥创造力，同时也能够检验学生的实际操作能力。
5. 附录
5.1 程序源码
见电子压缩文档2048_R.zip和2048_L.zip文件
5.2 其他
若有其他附录文件，可写于此处，组织好格式
