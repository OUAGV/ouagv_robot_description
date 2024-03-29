# ouagv_robot_description
## environment
- ROS2 Humble
- Ubuntu 22.04

# usage
```
ros2 launch ouagv_robot_description show_diff_robot.launch.py
```
で
- gazebo
- rviz
- ros2_control

が立ち上がる

## publish  
- /diff_drive_base_controller/odom
- /scan
- /imu/data

## subscribe
- /diff_drive_base_controller/cmd_vel_unstamped

## robot の parameter

- タイヤの半径 : 0.125(m)
  - diff_drive_controller の wheel_radius
  - xacro の wheel.urdf.xacro の radius
- タイヤ間の距離（車体の幅）: 0.6m(仮定)
  - diff_drive_controller の wheel_separation
  - xacro の diff_drive_robot.xacro の y の値

車体のサイズ制限は

- 幅: 0.75m
- 長さ 1.2m
- 高さ 0.6m 以上 1.5m 以下

ここでは仮定で

- 幅: 0.5m(タイヤ込)
  - タイヤ抜きだと 0.33m
  - タイヤの幅は 1 つ 0.085m
- 長さ 0.5m
- 高さ 0.7m(一番高い部分で)

## gzclient が起動しない時

```
. /usr/share/gazebo/setup.sh
```

で治ることがある（なんで？）

参照: https://answers.ros.org/question/358847/cannot-launch-gzclient-on-a-launch-file-results-in-shared_ptr-assertion-error/

# 知見

diff_drive_controller の wheel_radius とか wheel_separation は URDF に基づいて

正確に値を渡さないと LaserScan がロボットと一緒に動くようになるエラーが起こる
