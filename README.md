# NavSR Dataset
## NavSR: A Multi-Modal Navigation Dataset for Service Robot with Comprehensive Ground Truth
##  📢Update
- [2025.10.30] Add configuration files for the algorithms evaluated in the paper!
- [2025.10.28] Create the NavSR Repository and add the calibration files!

## 👀Overview
![fig2total2](https://github.com/user-attachments/assets/334ee32f-3985-45f1-9a84-b679d08868f9)

<details>
<summary><b>Abstract</b></summary>
Service robots are usually deployed for autonomous operations in large office buildings and outdoor community scenarios. Due to the lack of reliable satellite signals and roadmaps in such environments, service robots should equip multiple perception sensors to achieve reliable autonomous navigation by performing tasks including SLAM, semantic perception, depth estimation, and so on. However, existing datasets for service
robots remain insufficient and often fall short of sensor diversity, ground truth variety, and ground truth accuracy, making them inadequate for the growing demands of algorithm development and evaluation. To address this gap, this paper presents NavSR, a multi-modal dataset designed for service robots in office blocks and community settings. A wide range of strictly synchronized and geometrically calibrated data are provided, including stereo RGB and grayscale images, event vision, rotating and solid-state lidar scans, consumer- and industrial-grade IMU series, and wheel odometry. The dataset consists of 24 sequences covering 15.9 km of trajectories and includes challenging conditions such as varying illumination, low texture, long corridors, narrow pathways, and dynamic objects. We provide high-precision localization ground truth based on pre-built survey maps, as well as finegrained semantic annotations and depth map ground truth. We have conducted comprehensive tests on the latest multi-sensor fusion and new-paradigm SLAM systems, semantic segmentation, and depth estimation algorithms in the field, demonstrating the high applicability of the dataset.
</details>

<details>
<summary><b>Main Contributions</b></summary>
<ul>
<li>We fulfill the pressing dataset demands in service robot field by providing NavSR, which captures challenging and highly representative environments in indoor large office building and outdoor community areas. Diverse and complex features are covered inside, making it suitable for evaluation of robustness and practical performance of algorithms.</li>
<li>We enable versatile benchmarking of cutting-edge multimodal and new-paradigm algorithms on our dataset by providing a rigorously calibrated and synchronized multi-sensor configuration, integrating stereo RGB and grayscale cameras, stereo simulated event vision, spinning and MEMS LiDARs, dual-grade IMUs, and wheel odometry.</li>
<li>We are the first multi-modal navigation dataset in service robot domain that provides such comprehensive and highquality ground truth data, including cm-level localization from survey maps, fine-grained semantic segmentation annotations, and accurate LiDAR-projected dense depth maps.</li>
</details>

<details>
<summary><b>Sensor Setup</b></summary>
| Sensor | Model | Frequency | ROS Topic | ROS Message Type | Characteristics |
|--------|-------|-----------|-----------|------------------|-----------------|
| Stereo Gray | DALSA M1930 | 40Hz/10Hz | `/dalsa_gray/left/image_raw`<br>`/dalsa_gray/right/image_raw` | sensor_msgs/Image | Global shutter, ≤5ms exposure<br>1920×1200/960×600, 71°×56° FoV |
| Stereo RGB | DALSA C1930 | 40Hz/10Hz | `/dalsa_color/left/image_raw`<br>`/dalsa_color/right/image_raw` | sensor_msgs/Image | Global shutter, ≤10ms exposure<br>1920×1200/960×600, 71°×56° FoV |
| Spinning LiDAR | Velodyne VLP16 | 10Hz | `/velodyne_points` | sensor_msgs/PointCloud2 | 16 channels, 360°×30° FoV<br>±3cm@100m range |
| MEMS LiDAR | Livox AVIA | 10Hz | `/livox/lidar` | livox_ros_driver/CustomMsg | Non-repetitive, 70°×77° FoV<br>±2cm@200m range |
| Consumer IMU | BMI088 | 200Hz | `/livox/imu` | sensor_msgs/Imu | 6-axis, Livox built-in<br>Bias: 1°/s (Gyro), 20 mg (Acc) |
| Industrial INS | Xsens Mti-680G | 400Hz | `/imu/data` | sensor_msgs/Imu | 9-axis, with orientation<br>Bias: 8°/h (Gyro), 0.01 mg (Acc) |
| Stereo Event | v2e Simulator | - | `/davis_left`<br>`/davis_right` | dvs_msgs/EventArray | 960×600, aligned with DALSA |
| Wheel Odometry | Scout V1.0 | 200Hz | `/odom` | nav_msgs/Odometry | 4-wheel-drive, 3-axis, 1024-line |
| 3D Survey Scanner | Leica RTC360 | - | - | - | 0.5m-130m range<br>1mm+10ppm accuracy |
</details>


<details>
<summary><b>Sensor Setup</b></summary>

</details>

