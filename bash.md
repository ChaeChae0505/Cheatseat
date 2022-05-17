#============================================================================
#User system setting  added
alias up='sudo apt-get update && sudo apt-get upgrade -y'
alias re='sudo reboot'
alias cc='clear'
alias halt='sudo halt -p'
alias eb='sudo gedit ~/.bashrc'
alias vb='sudo vi ~/.bashrc'
alias sb='source ~/.bashrc'
alias mh='sudo mount /dev/sda ~/data'

export PATH=/usr/local/cuda-11.0/bin:$PATH
export PATH=$PATH:/usr/local/cuda-11.0/bin
export LD_LIBRARY_PATH=/usr/local/cuda-11.0/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.0/lib64
export CUDADIR=/usr/local/cuda-11.0

#============================================================================

#============================================================================
# ROS1
source /opt/ros/noetic/setup.bash
source ~/zed_ros1_ws/devel/setup.bash
source ~/vio_ws/devel/setup.bash
source ~/sim_ws/devel/setup.bash
source ~/test_ws/devel/setup.bash

# export PX4-GAZEBO path
export GAZEBO_PLUGIN_PATH=$GAZEBO_PLUGIN_PATH:~/sim_ws/PX4-Autopilot/build/px4_sitl_default/build_gazebo
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/sim_ws/PX4-Autopilot/Tools/sitl_gazebo/models
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/sim_ws/PX4-Autopilot/build/px4_sitl_default/build_gazebo
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/sim_ws/PX4-Autopilot
export ROS_PACKAGE_PATH=$ROS_PACKAGE_PATH:~/sim_ws/PX4-Autopilot/Tools/sitl_gazebo
# export additional GAZEBO models
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/sim_ws/src/gazebo_models
export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:~/sim_ws/src/uv-rl-sim/worlds/worlds_data/models

# IP settings for connection with husky
#export ROS_IP=192.168.1.123
#export ROS_MASTER_URI=http://192.168.1.123:11311
# export ROS_IP=10.42.0.10
# export ROS_MASTER_URI=http://10.42.0.232:11311
#============================================================================

#============================================================================
#about ROS2
#export LANG=en_US.UTF-8
# source /opt/ros/foxy/setup.bash
# source ~/nav2_tb_ws/install/setup.bash
# source ~/carto_ws/install/setup.bash
# source ~/zed_ws/install/setup.bash
#export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/home/ros2/nav2_tb_ws/src/nav2_tb_example/models
#export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/home/ros2/nav2_tb_ws/src/nav2_tb_outdoor/models
#export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/home/ros2/nav2_tb_ws/src/gazebo_models
#export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:/home/ros2/nav2_tb_ws/src/px4_models
#============================================================================

# ROS noetic
alias ros1="source /opt/ros/noetic/setup.bash && source ~/box_detect_ws/devel/setup.bash"
alias zed2='roslaunch zed_wrapper zed2.launch'
alias husky='ssh husky@192.168.1.11'
alias kg='pkill -9 gzserver && pkill -9 gzclient'

# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/ros2/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/ros2/anaconda3/etc/profile.d/conda.sh" ]; then
        . "/home/ros2/anaconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home/ros2/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

export TERMINFO=/usr/share/terminfo 
