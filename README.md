## 准备工作
* 运行`git clone https://git.oschina.net/jiangxihj/exercise_ec_ws`下载代码
* 安装相关依赖项，依次执行下列指令
 
```
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get update
sudo apt-get install ros-indigo-map-server
sudo apt-get install ros-indigo-move-base
sudo apt-get install ros-indigo-navigation
```
 
* 运行`cd exercise_ec_ws`进入exercise_ec_ws文件夹，运行`catkin_make`编译
* `注意`：每次打开一个新的termianl，记得要运行`source devel/setup.bash`
 
## Exercise 1： 路径规划
# 问题描述
* 简介：给定二维栅格地图，栅格地图中根据激光数据标记障碍物信息。实验人员需要实现一种路径规划方法，输入栅格地图中机器人当前位置与目标位置，输出能够到达目标位置的安全路径。

* 具体工作：编写路径规划函数`pathPlan`。该函数位于`src/exercise_1/src/car_move.cpp`文件中。

* 函数接口如下
```
vector<string> pathPlan(vector< vector<string> > inputMap, 
                                        vector< vector<int> > inputObstacle, 
                                        string startPoint, 
                                         string targetPoint);
```

> **输入**

`inputMap`: 环境栅格地图，以二维数组形式表示，每一个元素代表地图上该点编号；`特别说明：` 数组中元素Ax_y代表地图中坐标位置（x*0.1, y*0.1）的点，如A1_1代表位置（0.1, 0.1）的点

`inputObstacle`: 环境障碍物信息，二维数组形式表示，元素为0表示无障碍，元素为1表示有障碍

`startPoint`: 路径规划起始点，以地图上编号表示

`targetPoint`: 路径规划终点，以地图上编号表示

> **返回值**

返回值类型vector<string>，每个元素代表由当前位置到目标位置需要经过的栅格坐标编号


# 仿真环境启动步骤
* 启动可视化界面
 
```
roslaunch exercise_1 exercise_1.launch
```
左上角点击file，选择Open Config，然后选择exercise_1文件夹下nav.rviz文件。可视化界面中会显示机器人当前位置和栅格地图，白色长方体代表机器人当前位置，红色方块代表地图中非障碍点，绿色方块代表地图中障碍点。
 
* 编写路径规划函数`pathPlan`。

* 修改完，运行`catkin_make`编译通过后，运行该程序
 
```
rosrun exercise_1 exercise_1_node
```
在可视化界面中可以看到计算出的轨迹（界面中绿线表示）。移动机器人沿该轨迹运动

## Exercise 2： 轨迹规划
# 问题描述
* 简介：给定一系列路径点，机器人当前位置、方向与速度，实验人员需要计算一系列轨迹运动控制指令，使机器人能够实现经过指定路径点运动，同时确保运动平滑且尽可能减少原地转向。

* 具体工作：编写路径规划函数`trajectoryPlan`。该函数位于`src/exercise_2/src/car_move.cpp`文件中。

* 函数接口如下
```
vector< vector<double> > trajectoryPlan( vector< double > viapoint_x, vector< double > viapoint_y,
        double current_x, double current_y, double current_orientation,
        double current_v, double current_vomega,
        double period,
        double command_length);
```

> **输入**

`viapoint_x`: 路径点x轴坐标序列

`viapoint_y`:路径点y轴坐标序列

`current_x`:机器人当前位置x轴坐标

`current_y`:机器人当前位置y轴坐标

`current_orientation `: 机器人当前朝向角

`current_v `: 机器人当前平移速度

`current_vomega `: 机器人当前旋转速度

`period `: 控制周期，即两次控制指令发送间隔

`command_length`: 一次计算的控制指令条数


> **返回值**

返回值类型vector< vector<double> >，每个元素为二元数组，表示该时刻机器人的平移速度和旋转速度控制指令

# 仿真环境启动步骤
* 启动可视化界面
 
```
roslaunch exercise_2 exercise_2.launch
```
左上角点击file，选择Open Config，然后选择exercise_2文件夹下nav.rviz文件。可视化界面中会显示机器人当前位置，以白色长方体代表
 
* 编写路径规划函数`trajectoryPlan`。

* 修改完，运行`catkin_make`编译通过后，运行该程序
 
```
rosrun exercise_2 exercise_2_node
```
在可视化界面中可以看到所有路径点（红色方块表示）和计算出的运动轨迹（界面中绿线表示）。移动机器人沿该轨迹运动
 
 
 
 
 
 
 
 
 
 
 
 
 
 
