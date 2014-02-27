traffic-simulation
==================

交通模拟系统仿真

一、问题描述
用面向对象方法和面向对象程序设计语言，实现满足下述要求的一个交通活动仿真程序。
在太白路立交建成之前，我校北门二环路有若干十字路口，取其中2个加以考察：以下分别称二环－白沙路口和二环－太白路口为 CR1 和CR2，路口的红绿灯如图所示。分别称图中的二环路东、西端点为EHE 和EHW，白沙路的南、北端点为BSS 和BSN，太白路的南、北端点为TBS 和TBN。

约束：
1) 红绿灯组（①，④）、（②，③）、（⑤，⑧）、（⑥，⑦）分别同步动作；
2) 绿灯行，红灯停，黄灯忽略。当汽车位于路口的第一位置时，遇红灯允许右转弯，
也允许绕隔离区掉头（参见约束7））；
3) 红绿灯组（①，④）、（⑤，⑧）的控制规则为：绿灯亮20 秒后红灯亮120 秒。红
绿灯组（②，③）、（⑥，⑦）的规则相反；
4) 路口间放行规则为：红绿灯组（②，③）变为绿灯后60 秒，（⑥，⑦）变为绿灯。
红绿灯组（①，④）变为绿灯后60 秒，（⑤，⑧）变为绿灯。
5) 各区间的车行时间分别为（与车行方向无关）
6) 为简化问题，所有道路均不允许车辆并行（在路口掉头车辆可与路口直行车辆同
时通过，见约束8）），车辆的最小车间距相当于1 秒的车行时间。
7) 按照市公安局最新规定，二环路的所有路口均禁止左转弯，欲左转弯的车辆应按
下图所示的行驶路线行进：
8) 掉头车辆不占用对应路口的直行车道，可同时通行（例如，二环路上自西向东的车辆在CR2 掉头时，不影响CR2 自北向南的直行车道上的车辆通行。以此类推）。掉头后，如遇直行车辆，应让直行车辆先行（例如，上述车辆掉头后，如遇二环路上自东向西直行的车辆，应让其先行）。

应仿真的交通活动：
1) 在端点 BSN、EHW、BSS、TBN、TBS、EHE 随机产生汽车，前往端点BSN、EHW、BSS、TBN、TBS、EHE 中非起点的任一端点（例如从BSN 出发的汽车，可前往EHW、BSS、TBN、TBS、EHE）。若所产生的汽车在没有通过最近的十字路口时，已经出现饱和，则暂停产生，至非饱和状态再开始产生；
2) 在端点 BSN、BSS、TBN、TBS 产生汽车的频度，是端点EHW、EHE 产生汽车频度的1/3。
开发结果的行为特征：
1) 有简单的界面，体现汽车、道路、路口、红绿灯随时间变化的状态（能说明问题即可，切忌把主要精力放在界面上）；
2) 仿真应符合上面的约束和要求；
3) （选做）可以调整某些时间参数（如红绿灯持续时间、路口间放行规则所涉及的
时间参数、以及你想改变的其他参数），再观察所引起的变化。

二、类的设计
经过分析，初步认为至少应该有车类，路灯类，路类，界面类这四个类。其中车类是这四个类中最需要精心设计的一个类，它包含车如何移动，红绿灯的判断，是否和前一个车碰撞的判断，是否是拐点等，路灯类则决定CR1和CR2路口的红绿灯状态，路类负责根据起始点和终点生成一条车要走的路。界面表示类则负责对整个结果进行完整的清晰的表示，同时应控制模拟仿真过程中的一系列操作，作为主控流程来出现。
在此基础上我进行了初步的设计和进一步的分析，发现抽象出文档类的必要性，因为界面类需要完成车、路、红绿灯的动态显示和刷新，并且要控制汽车的产生频率，路面拥塞的控制等，有必要抽象出一个文档类，主要为界面提供所需要的数据。
其次，在选做部分，提到了可以调整某些时间参数（如红如红绿灯持续时间、路口间放行规则所涉及的时间参数、以及你想改变的其他参数），再观察所引起的变化。此时需要一个新的界面，供用户输入相关参数。因此，需要一个设置类供用户输入参数。
以上就是对问题进行分析后的大体设计思路。

