## 安装教程
教程中使用的国外源下载，可更换为国内源加快下载速度
[Ubuntu （deb packages） — ROS 2 文档：Humble 文档](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)

## 使用步骤
### 1.创建工作空间
1. 创建一个自命名文件夹/文件夹/src
	mkdir -p Learn_ROS2/L01_helloworld/src

2. 进入工作空间
	cd Learn_ROS2/L01_helloworld

3. 编译
	colcon build

4. 编译结果
	会生成三个文件夹
	build：存储编译文件的目录，该目录会为每个功能包创建一个单独的子目录。
	install：安装目录，存储已经编译的功能包生成的可执行文件。
	log：日志目录，存储日志文件。
	src：自己创建的，一般用于存储功能包源码。
### 2.创建功能包
1. 进入工作空间/src
	cd Learn_ROS2/L01_helloworld/src

2. 执行创建命令
	创建命令格式
	ros2 pkg create [--build-type] 功能包类型 功能包名 [--dependencies] 依赖包名 [--node-name] 可执行节点名
	
	示例
	创建功能包
	ros2 pkg create helloworld_cpp --build-type ament_cmake --node-name helloworld_node --dependencies rclcpp

%% 创建一个helloworld_cpp的功能包，类型为ament_cmake，python包类型为ament_python。也就是c++类型的包，同时创建一个名为helloworld_node的节点，指定依赖包为rclcpp %%。
### 3.编写源代码
1.  编写程序代码
	include "rclcpp/rclcpp.hpp"
	
	int main(int argc,char ** argv){
		rclcpp::init(argc,argv);
		auto node=rclcpp::Node::make_shared("helloworld_node");
		RCLCPP_INFO(node->get_logger(),"Hello World!");
		rclcpp::shutdown();
		return 0;
	}
### 4.设置编译规则
创建功能包时已经编译完成了，后期可根据需求设置功能包的相应配置文件。
### 5.编译与调试
1. 回到工作空间，执行编译生成相应的可执行文件和库
	colcon build

%%
每编译一个功能包时执行这个命令会同时把所有功能包进行编译，效率很慢。
可指定功能包编译，命令如下：
colcon build --packages-select 功能包1 功能包2 ........功能包n
%%

2. 设置环境变量
	. install/setup.bash
	source install/setup.bash
	source ./install/setuo.bash
	.和source等价，这是设置一次性变量，可把这条命令保存到系统的.bashrc配置文件中进行永久配置。

%% 
持久化配置
每次执行相应节点时，都需要调用. install/setup.bash命令，不方便。可将该命令的调用添加进~/.bashrc配置文件中。
命令如下：
echo "source /{工作空间路径}/install/setup.bash" >> ~/.bashrc 
%%

### 6.功能运行
1. 运行程序
	运行ros2功能包的通用命令
	ros2 run 功能包名 功能包节点名 [可选参数]
	
	ros2 run helloworld_cpp helloworld_node 