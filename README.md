# Moving End-Effectors by Deep Reinforcement Learning for Better Hand-Eye Calibration Performance 


## 1. Usage

Our code is tested on Ubuntu 20.04 and ROS Noetic.

### 1.1 Build Instructions

- Conda environment
```
conda env create -f hec.yaml
```

### 1.2 Gazebo simulation

If you want to use kinova gen3_lite manipulator, you should follow [ros_kortex](https://github.com/Kinovarobotics/ros_kortex).

- After Installation, Clone the gazebo repository and catkin make:
```
mkdir catkin_ws
cd catkin_ws
git clone https://github.com/Seunghui-Shin/Better-HEC-by-DRL.git
mkdir src
mv -r Better-HEC-by-DRL/ros_kortex src/
rm -rf Better-HEC-by-DRL/
cd ~/catkin_ws && catkin_make
```

### 1.3 Pose Network and Policy

If you want to use DenseFusion for pose network, yo should follow [DenseFusion](https://github.com/j96w/DenseFusion).

Also, you sholud follow [Discrete SAC](https://github.com/BY571/SAC_discrete) and [Learn-to-Calibrate](https://github.com/ethz-asl/Learn-to-Calibrate/tree/master?tab=readme-ov-file) for DRL.

- After Installation, Clone the repository and catkin build:
```
mkdir robot_ws
cd robot_ws
mkdir src
cd src
git clone https://github.com/Seunghui-Shin/Better-HEC-by-DRL.git
cd Better-HEC-by-DRL
rm -rf ros_kortex
cd ../..
catkin build
```

- Kinova Gen3 Lite end-effector weights are [here](https://drive.google.com/drive/u/1/folders/1eSech0IvzmTBDrLPPm-NSky1l2skHeAF).
- You should move the weights to DenseFusion_Pytorch_1_0/weights/dis.


## 2. Running the code

### 2.1 Gazebo simulation
```
roslaunch kortex_gazebo spawn_kortex_robot_realsense.launch arm:=gen3_lite
```
   
### 2.2.1 Training
```
conda activate hec
cd robot_ws/src/Better-HEC-by-DRL/hec
python3 python/train_policies/RL_algo_kinova_discrete_sac.py
```
### 2.2.2 Testing
```
conda activate hec
cd robot_ws/src/Better-HEC-by-DRL/hec
python3 python/test_policies/RL_algo_test_kinova_discrete_sac.py
```

### 2.2 Pose Network and Robot Control
```
conda activate hec
cd robot_ws/src/Better-HEC-by-DRL
./DenseFusion_Pytorch_1_0/tools/train.sh
```
We use Kinova Gen3 Lite manipulator and DenseFusion for posenet.

So, refer to the code to integrate your robot with the desired posenet.

## 3. License

License under the [MIT Ricense](https://github.com/Seunghui-Shin/Better-HEC-by-DRL/blob/main/DenseFusion_Pytorch_1_0/LICENSE)

License under the [Kinova inc](https://github.com/Seunghui-Shin/Better-HEC-by-DRL/blob/main/ros_kortex/LICENSE)


## 4. Code reference:

Our code is based on the following repositories:

- [ros_kortex](https://github.com/Kinovarobotics/ros_kortex)
- [realsense](https://github.com/issaiass/realsense2_description)
- [ArUco marker](https://github.com/ValerioMagnago/aruco_description)
- [DenseFusion](https://github.com/j96w/DenseFusion)
- [Discrete SAC](https://github.com/BY571/SAC_discrete)
- [Learn-to-Calibrate](https://github.com/ethz-asl/Learn-to-Calibrate/tree/master?tab=readme-ov-file)
