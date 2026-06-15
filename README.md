# pairs_vins_imu_filter

Cleans up raw IMU data before it is fed to visual-inertial (VINS/VIO) state estimation. It applies notch and IIR (Butterworth) filters to the accelerometer and gyroscope streams to suppress motor vibration and structural resonance, which would otherwise corrupt the odometry estimate. It can read a combined IMU topic or separate accel/gyro topics and republishes a single filtered `sensor_msgs/Imu`. This is part of the PAIRS estimation layer.

## Contents

- `VinsImuFilter` nodelet — subscribes to `imu_in` (or separate `accel_in` / `gyro_in`), filters each axis with configurable notch and IIR filters, and publishes the result on `imu_out`.
- Per-sensor tuning configs under `config/` (`t265`, `oak`, `icm_42688`, `mavros`).
- Helper filter-design scripts in `scripts/` (`filter_design.py`, `butterworth_filter_design.m`).

## Branches

- `ros1` — ROS 1 Noetic (catkin)
- `ros2` — ROS 2 Jazzy (ament_cmake)

## Install (ROS 1 Noetic)

```bash
sudo apt install ros-noetic-pairs-vins-imu-filter
```

## Usage

Launch the filter for the IMU source you are using:

```bash
roslaunch pairs_vins_imu_filter filter_t265.launch
roslaunch pairs_vins_imu_filter filter_oak.launch
roslaunch pairs_vins_imu_filter filter_icm_42688.launch
roslaunch pairs_vins_imu_filter filter_mavros.launch
```

## License
BSD 3-Clause. Derived from the CTU-MRS `pairs_vins_imu_filter` package; the original
copyright is retained in [LICENSE](LICENSE).
