# 论文目的
解决两个问题   
(1) How should we design the reward so that one can guarantee to minimize the travel time?   
(2) How to design a state representation which is concise yet sufficient to obtain the optimal solution?
# 论文方法
## state
Entering direction:‘W’, ‘E’, ‘N’, ‘S’  
Signal Phase: Left, Through, and Right (‘L’, ‘T’, and ‘R’ for short)  
一个信号阶段可以表示为A1B1-A2B2，其中Ai表示进入方向，Bi表示信号灯类型。例如WT-ET表示东西方向是绿灯，其余所有方向都是红灯。  
The state includes the number of vehicles vj,t on each lane j and the current signal phase pt. 
## action
给定一系列信号灯阶段(p0, p1, p2, ..., pK-1)，每一个timestamp t都要决定是否进入下一个阶段（action = 1 or action = 0）
## reward
使用当前路口队列长度作为奖励函数（等价于在运输方法中最优化travel time）

