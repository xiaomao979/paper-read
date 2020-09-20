# 论文目的
采⽤RL来解决当前的交通信号灯控制系统难以根据动态的路况信息做出实时调整这⼀问题.
⽬前的RL⽅法对state的描述都⽐较简单，⼀般仅仅将当前状态的交通流量作为state，
这样会产⽣部分观测的问题，即实际environment下的state S 和观测得到的state O之间的差异过⼤，
那么学习到的策略policy其实就不能很好地适⽤于实际的environment。
# 论文方法
采⽤了RL的⽅法⽤DQN去学习value以及policy，
其主要的特点在于由offline和 online learning两部分组成的model framework
以及使⽤了被称作“Phase Gate”的Q-Network以及与此相对应的较为复杂的state以及reward描述。
## state
根据每个车道，获取每个车道i上的排队长度Li 信息，
车道上的总的车辆数Vi，根据当前模型计算出来的等待时间Wi ，
并且根据图像分析得到的每辆车的位置信息M，还有当前的信号灯状况Pc 以及下一个状态的信号灯状况Pn 
## action
这⾥把实际中的红绿灯切换过程做了简化，action只有两种可能情况，即0保持当前状况与1改变当前状况。
## reward
reward分为六个部分总和：  
1. Sum of queue length L over all approaching lanes 
2. Sum of delay D over all approaching lanes
3. Sum of updated waiting time W over all approaching lanes
4. Indicator of light switches C, where C = 0 for keeping the current phase, and C = 1 for changing the current phase
5. Total number of vehicles N that passed the intersection during time interval ∆t after the last action a
6. Total travel time of vehicles T that passed the intersection during time interval ∆t after the last action a
