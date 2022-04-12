1. 进入docker容器
```
cd /path/to/ODM
DATA=/path/to/datasets REPOS=/path/to/anywhere IMAGE=ubuntu2004-odm ./start-dev-env.sh
```
进入容器后，user默认为root，ODM代码装载到/code，数据集目录装载到/datasets，REPOS指定的目录（如PX4代码库）装载到/repos，ros2、QGroundControl等放在/home/robot目录

2. 进入ODM库，尝试编译代码并运行（运行方式参照readme）
```
cd /code
bash configure.sh install
./run.sh --project-path /datasets odm_data_aukerman  # 需下载aukerman数据集并放到宿主机的数据集目录下
```
因为版本问题，默认安装的opencv-python可能是python3.9的，但容器内使用的是python3.8，如果运行时碰到import cv2的问题，需把SuperBuild/install/lib/python3.9删除，避免版本混乱的问题

3. 运行PX4仿真
```
tmux  # 进入tmux，便于运行多个命令行窗口
cd /repos/PX4-Autopilot
make px4_sitl gazebo_typhoon_h480  # 运行gazebo
ctrl-b "  # 新建tmux窗口（关于tmux的使用方式，自行搜索）
su -c bash robot  # 切换到robot用户，在默认的root用户下无法运行QGroundControl
cd
./QGroundControl.AppImage
```

4. 关于翻墙
因为GFW的关系下载github库的时候可能会碰到问题，ubuntu下的翻墙软件自行查找。我的方式是在宿主机上设置代理并绑定到127.0.0.1:8890，docker容器会公用宿主机的网络，export https_proxy=127.0.0.1:8890即可在docker容器内翻墙
