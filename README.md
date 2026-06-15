# pairs_vins_imu_filter

Cleans up raw IMU data before it is fed to visual-inertial (VINS/VIO) state estimation. It applies notch and IIR (Butterworth) filters to the accelerometer and gyroscope streams to suppress motor vibration and structural resonance, which would otherwise corrupt the odometry estimate. It can read a combined IMU topic or separate accel/gyro topics and republishes a single filtered `sensor_msgs/Imu`. This is part of the PAIRS estimation layer.

## Contents

- `vins_imu_filter::VinsImuFilter` composable node — subscribes to `imu_in` (or separate accel/gyro inputs), filters each axis with configurable notch and IIR filters, and publishes the result on `imu_out`.
- Per-sensor tuning configs under `config/` (`t265`, `oak`, `icm_42688`, `mavros`).
- Helper filter-design scripts in `scripts/` (`filter_design.py`, `butterworth_filter_design.m`).

## Branches

- `ros1` — ROS 1 Noetic (catkin)
- `ros2` — ROS 2 Jazzy (ament_cmake)

## Install (ROS 2 Jazzy)

```bash
sudo apt install ros-jazzy-pairs-vins-imu-filter
```

## Usage

Launch the filter for the IMU source you are using:

```bash
ros2 launch pairs_vins_imu_filter filter_t265.launch.py
ros2 launch pairs_vins_imu_filter filter_icm_42688.launch.py
ros2 launch pairs_vins_imu_filter filter_simulation.launch.py
```

## License
BSD 3-Clause. Derived from the CTU-MRS `pairs_vins_imu_filter` package; the original
copyright is retained in [LICENSE](LICENSE).
