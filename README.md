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
<summary><b>Data Sequence</b></summary>
Here is the overall organization of the NavSR dataset. The dataset includes separate directories for indoor and outdoor scenes, each containing timestamp files (.txt), raw images in TIFF format, and rosbags with multiple sensors: the "*VLIO.bag" file contains images, point clouds, and IMU data, while "*LIO.bag" file excludes image data. Event streams are stored in "*ESVIO.bag" file. Semantic segmentation labels and depth maps are provided in PNG format. Furthermore, both the extrinsic and intrinsic parameters of all sensors are provided to support accurate sensor fusion and calibration. We also include configuration files for various algorithms tested on the NavSR dataset.

<img width="700" height="640" alt="data_organ" src="https://github.com/user-attachments/assets/b5ce8492-055c-40a6-a696-1aa0f6f165c5" />

The dataset consists of 24 sequences covering 15.9 km of trajectories and includes challenging conditions such as varying illumination, low texture, long corridors, narrow pathways, and dynamic objects. The following table shows summary of all sequences statistics in the NavSR dataset.
| Scene | Sequence | Time | Size/GB | Length/m | Duration/s | Description |
|-------|----------|------|---------|----------|------------|-------------|
| **Indoor** (Office buildings) | I_1010_00 | 2022-10-10-21-28-30 | 24.3 | 530.8 | 481.7 | Night/Low Light/Dark/Sharp Turn/Return Path |
| | I_1010_01 | 2022-10-10-21-39-03 | 25.0 | 579.8 | 499.2 | Night/Low Light/Sharp Turn/Return Path |
| | I_1010_02 | 2022-10-10-21-50-28 | 26.3 | 615.6 | 516.5 | Night/Low Light/Sharp Turn/Wheel Slippage |
| | I_1010_03 | 2022-10-10-22-01-18 | 41.7 | 923.8 | 808.2 | Night/Low Light/Dark/Sharp Turn/Wheel Slippage |
| | I_1010_04 | 2022-10-10-22-18-25 | 13.8 | 316.9 | 280.9 | Night/Low Light |
| | I_1017_00 | 2022-10-17-15-22-55 | 15.5 | 349.5 | 326.9 | Afternoon/HDR/Sharp Turn/Wheel Slippage |
| | I_1017_01 | 2022-10-17-15-30-03 | 16.7 | 407.2 | 335.7 | Afternoon/HDR/Dynamic |
| | I_1017_02 | 2022-10-17-15-37-44 | 45.0 | 1106.1 | 869.2 | Afternoon/Low Light/HDR/Sharp Turn |
| | I_1017_03 | 2022-10-17-15-53-54 | 27.0 | 680.2 | 531.1 | Afternoon/Low Light/HDR/Sharp Turn/Return Path |
| | I_1017_04 | 2022-10-17-16-08-37 | 31.5 | 791.9 | 610.1 | Afternoon/Low Light/HDR/Sharp Turn |
| **Outdoor** (Community areas) | O_1008_00 | 2022-10-08-13-33-21 | 25.9 | 665.8 | 511.4 | Afternoon/Sports Field |
| | O_1008_01 | 2022-10-08-14-08-31 | 36.6 | 952.1 | 721.5 | Afternoon/HDR/Narrow Path |
| | O_1008_02 | 2022-10-08-14-22-57 | 36.3 | 932.4 | 710.9 | Afternoon/HDR |
| | O_1009_00 | 2022-10-09-14-58-41 | 34.1 | 835.6 | 709.1 | Afternoon/HDR/Sports Field/Sharp Turn |
| | O_1009_01 | 2022-10-09-15-13-13 | 39.7 | 977.1 | 778.9 | Afternoon/Sports Field/Narrow Path |
| | O_1009_02 | 2022-10-09-15-51-44 | 39.6 | 945.9 | 788.0 | Afternoon/Sports Field |
| | O_1009_03 | 2022-10-09-16-16-37 | 37.9 | 911.1 | 744.1 | Afternoon/HDR/Narrow Path |
| | O_1017_00 | 2022-10-17-11-38-18 | 10.9 | 266.9 | 244.6 | Noon/HDR/Crowd/Dynamic |
| | O_1017_01 | 2022-10-17-11-44-17 | 18.6 | 465.8 | 387.7 | Noon/Crowd/Dynamic |
| | O_1017_02 | 2022-10-17-11-52-32 | 22.8 | 545.6 | 465.8 | Noon/Crowd/Dynamic |
| | O_1017_03 | 2022-10-17-12-02-55 | 25.3 | 637.2 | 514.5 | Noon/Crowd/Dynamic |
| | O_1017_04 | 2022-10-17-12-19-53 | 20.8 | 532.2 | 419.6 | Noon/Crowd/Dynamic |
| | O_1017_05 | 2022-10-17-12-37-26 | 15.8 | 400.9 | 340.8 | Noon/Sports Field |
| | O_1017_06 | 2022-10-17-12-45-07 | 22.5 | 566.1 | 455.6 | Noon/Narrow Path/Sports Field |
</details>


<details>
<summary><b>Ground Truth</b></summary>
<ul>
<li>Ground Truth Trajectories</li>
NavSR employs a map-based ground-truth generation approach. The mapping process was carried out using a Leica RTC360 scanner, with 214 and 129 scan stations in the community and office building scenarios, respectively. Considering the accuracies of both the pre-mapping and localization processes, our groundtruth generation pipeline provides cm-level global accuracy.
<img width="600" height="500" alt="bfe666e6-ceab-4ddd-b11e-b1ab1954e1da" src="https://github.com/user-attachments/assets/b8bdcf8c-645f-4072-a5f7-6fe4864a5c2c" />


<li>Depth Maps</li>
We presents a novel depth estimation dataset constructed using two types of LiDAR sensors, namely the VLP-16 and Livox Avia. The dataset covers both indoor and outdoor scenes and comprises over 24k frames of semidense depth images. Here is the visualization of depth maps generated from accumulated LiDAR point clouds. 

<img width="2426" height="518" alt="image" src="https://github.com/user-attachments/assets/72062278-c7ad-4012-8b16-7985941ba44d" />

<li>Semantic Labels</li>
Overview of semantic segmentation categories and representative samples. Left: Distribution of semantic segmentation labels in the NavSR dataset. Right: Visualizations of instance samples for some typical semantic categories.
<img width="2862" height="802" alt="image" src="https://github.com/user-attachments/assets/50fbe69a-374d-45cc-85b4-88ef26ca6818" />

</details>

<details>
<summary><b>Algorithm Evaluation</b></summary>
We presents a comprehensive evaluation of state-of-the-art robotic navigation and perception algorithms, including conventional SLAM, emerging Neural- and 3DGS-based SLAM paradigms, event-based SLAM, depth estimation,
and semantic segmentation models.  
<li>Conventional SLAM: <a href="https://github.com/UZ-SLAMLab/ORB_SLAM3" target="_blank" rel="noopener">ORB-SLAM3</a>, 
  <a href="https://github.com/HKUST-Aerial-Robotics/VINS-Mono" target="_blank" rel="noopener">VINS-Mono</a>, 
  <a href="https://github.com/HKUST-Aerial-Robotics/A-LOAM" target="_blank" rel="noopener">LOAM</a>, 
  <a href="https://github.com/hku-mars/FAST_LIO" target="_blank" rel="noopener">FAST-LIO2</a>, 
  <a href="https://github.com/Cc19245/LVI-SAM-Easyused" target="_blank" rel="noopener">LVI-SAM</a>, 
  <a href="https://github.com/hku-mars/r3live" target="_blank" rel="noopener">R3LIVE</a>, 
  <a href="https://github.com/hku-mars/FAST-LIVO2" target="_blank" rel="noopener">FAST-LIVO2</a>
</li>

<li>Neural- and 3DGS-based SLAM / Rendering: <a href="https://github.com/HuajianUP/Photo-SLAM" target="_blank" rel="noopener">Photo-SLAM</a>,
<a href="https://github.com/youmi-zym/GO-SLAM" target="_blank" rel="noopener">GO-SLAM</a>,
<a href="https://github.com/PRBonn/PIN_SLAM" target="_blank" rel="noopener">PIN-SLAM</a>,
<a href="https://github.com/APRIL-ZJU/Gaussian-LIC" target="_blank" rel="noopener">Gaussian-LIC</a>,
<a href="https://github.com/xieyuser/GS-LIVM", target="_blank" rel="noopener">GS-LIVM</a>,
<a href="https://github.com/muskie82/MonoGS", target="_blank" rel="noopener">Mono-GS</a>,
<a href="https://github.com/graphdeco-inria/gaussian-splatting", target="_blank" rel="noopener">3DGS</a>
</li>

<li>Event-based SLAM: 
<a href="https://github.com/NAIL-HNU/ESVO2" target="_blank" rel="noopener">ORB-SLAM3+ESVO2</a>, 
<a href="https://github.com/arclab-hku/PL-EVIO_open" target="_blank" rel="noopener">PL-EVIO</a>, 
<a href="https://github.com/arclab-hku/ESVIO" target="_blank" rel="noopener">ESVIO</a>
</li>

<li>Depth Estimation: </li> <a href="https://github.com/zhyever/Monocular-Depth-Estimation-Toolbox/tree/main/configs/simipu" target="_blank" rel="noopener">SimIPU</a>, 
<a href="https://github.com/zhyever/Monocular-Depth-Estimation-Toolbox/tree/main/configs/binsformer" target="_blank" rel="noopener">BinsFormer</a>, 
<a href="https://github.com/zhyever/Monocular-Depth-Estimation-Toolbox/tree/main/configs/depthformer" target="_blank" rel="noopener">DepthFormer</a>, 
<a href="https://github.com/zhyever/Monocular-Depth-Estimation-Toolbox/tree/main/configs/dpt" target="_blank" rel="noopener">DPT</a>, 
<a href="https://github.com/lukemelas/EfficientNet-PyTorch" target="_blank" rel="noopener">EfficientNet</a>, 
<a href="https://github.com/DepthAnything/Depth-Anything-V2" target="_blank" rel="noopener">DepthAnythingv2</a>

<li>Semantic Segmentation: <a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/fcn" target="_blank" rel="noopener">FCN</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/unet" target="_blank" rel="noopener">U-Net</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/deeplabv3" target="_blank" rel="noopener">DeepLab</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/pspnet" target="_blank" rel="noopener">PSPNet</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/upernet" target="_blank" rel="noopener">UperNet</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/mobilenet_v2" target="_blank" rel="noopener">MobileNet</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/vit" target="_blank" rel="noopener">ViT-S</a>, 
<a href="https://github.com/open-mmlab/mmsegmentation/tree/v1.1.0/configs/swin" target="_blank" rel="noopener">Swin-T</a>, 
<a href="https://github.com/dongbo811/AFFormer" target="_blank" rel="noopener">AFFormer</a>
</li>

</details>

## ✉️Contact
This dataset is provided for academic purposes.


## ✏️Citation
If our dataset helps your research, please cite:

