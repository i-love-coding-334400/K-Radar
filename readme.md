<p align="center">
  <img src = "./docs/imgs/readme_logo.png" width="60%">
</p>

`KAIST-Radar (K-Radar)` (provided by ['AVELab'](http://ave.kaist.ac.kr/)) is a novel large-scale object detection dataset and benchmark that contains 35K frames of 4D Radar tensor (4DRT) data with power measurements along the Doppler, range, azimuth, and elevation dimensions, together with carefully annotated 3D bounding box labels of objects on the roads. K-Radar includes challenging driving conditions such as adverse weathers (fog, rain, and snow) on various road structures (urban, suburban roads, alleyways, and highways). In addition to the 4DRT, we provide auxiliary measurements from carefully calibrated high-resolution Lidars, surround stereo cameras, and RTK-GPS. This repository provides the `K-Radar` dataset, annotation tool for 3d bounding boxes, and the visualization tool for showing the inference results and calibrating the sensors.

![image](./docs/imgs/kradar_examples.png)

The URLs listed below are useful for using the K-Radar dataset and benchmark:
* <a href="https://arxiv.org/abs/2206.08171"> K-Radar paper and appendix [arxiv] </a>
* <a href="https://www.youtube.com/watch?v=TZh5i2eLp1k"> The video clip that shows each sensor measurement dynamically changing during driving under the heavy snow condition </a>
* <a href="https://www.youtube.com/watch?v=ylG0USHCBpU"> The video clip that shows the 4D radar tensor & Lidar point cloud (LPC) calibration and annotation process </a>
* <a href="https://www.youtube.com/watch?v=ILlBJJpm4_4"> The video clip that shows the annotation process in the absence of LPC measurements of objects  </a>
* <a href="https://www.youtube.com/watch?v=U4qkaMSJOds"> The video clip that shows calibration results </a>
* <a href="https://www.youtube.com/watch?v=MrFPvO1ZjTY"> The video clip that shows the GUI-based program for visualization and neural network inference </a>
* <a href="https://www.youtube.com/watch?v=8mqxf58_ZAk"> The video clip that shows the information on tracking for multiple objects on the roads </a>

# K-Radar Dataset
This is the documentation for how to use our detection frameworks with K-Radar dataset.
We tested the K-Radar detection frameworks on the following environment:
* Python 3.9 (3.10+ does not support open3d.)
* Ubuntu 18.04/20.04
* Torch 1.10.1
* CUDA 11.3

## Updates
[2022-10-14] We have realized that the network-attached storage (NAS) download link is unstable. As such, we are preparing the Google Drive download link similar to our other project <a href="https://github.com/kaist-avelab/K-Lane">K-Lane</a>.

[2022-09-30] The `K-Radar` dataset is made available via a network-attached storage (NAS) <a href="https://kaistavelab.direct.quickconnect.to:54568/">download link</a>.

## Preparing the Dataset

* Via our server

1. To download the dataset, log in to <a href="https://kaistavelab.direct.quickconnect.to:54568/"> our server </a> with the following credentials: 
      ID       : kradards
      Password : Kradar2022
2. Go to the "File Station" folder, and download the dataset by right-click --> download.
   Note for Ubuntu user, there might be some error when unzipping the files. Please check the "readme_to_unzip_file_in_linux_system.txt".
3. After all files are downloaded, please arrange the workspace directory with the following structure:
```
KRadarFrameworks
├── annot_calib_tools
      ├── mfiles
      ├── dataset_utils
├── devkits
      ├── configs
      ├── datasets
      ├── models
      ├── pipelines
      ├── resources
      ├── uis
      ├── utils
├── kradar_dataset
      ├── kradar_0
            ├── 1
            ├── 2
            ...
      ├── kradar_1
            ...
            ├── 57
            ├── 58
├── logs
```

* Via Google Drive Urls

## Sequence composition

Each of the 58 sequences consists of listed files or folders as follows.
We add the explanation or usage next to each file or folder.
```
Sequence_number.zip (e.g. 1.zip)
├── cam-front: Front camera images
├── cam-left: Left camera images
├── cam-rear: Rear camera images
├── cam-right: Right camera images
├── cell_path: File to generate data from bag or radar ADC files (refer to the matlab file generation code.)
├── description.txt: 
├── info_calib:
├── info_label: 
├── info_label_rev: 
├── lidar_bev_image:
├── lidar_bev_image_origin:
├── lidar_point_cloud:
├── os1-128:
├── os2-64:
├── radar_bev_image:
├── radar_bev_image_origin:
├── radar_tesseract:
├── radar_zyx_cube:
├── time_info:
```

## Requirements

1. Clone the repository
```
git clone ...
```

2. Install the dependencies
```
pip install -r requirements.txt
```

## Train & Evaluation
* To train the model, prepare the total dataset and run
```
python train_gpu_0.py ...
```

* To evaluate the model, modifying the lines that we have noted and run
```
python eval_conditional_0.py ...
```

## Model Zoo

* (TBD)
RTNH, RTN4D for Radar
PointPillars, PV-RCNNv2 for Lidar

We only show the detection performance for the 'Sedan' class on this page.

Please refer to <a href="https://paperswithcode.com/dataset/k-radar">the Benchmark section of paperswithcode</a>.

## Annotation process

1. [Data generation process] (from rosbag and radar ADC files)
2. [Calibration process]

## GUI-based devkits

1. [Visualization]
2. [Inference]

## License
The `K-Radar` dataset is published under the CC BY-NC-ND License, and all codes are published under the Apache License 2.0.

## Acknowledgement
The K-Radar dataset is contributed by [Dong-Hee Paek](http://ave.kaist.ac.kr/bbs/board.php?bo_table=sub1_2&wr_id=5), [Kevin Tirta Wijaya](http://ave.kaist.ac.kr/bbs/board.php?bo_table=sub1_2&wr_id=7), [Dong-In Kim](http://ave.kaist.ac.kr/bbs/board.php?bo_table=sub1_2&wr_id=13), [Min-Hyeok Sun](http://ave.kaist.ac.kr/bbs/board.php?bo_table=sub1_2&wr_id=14), advised by [Seung-Hyun Kong](http://ave.kaist.ac.kr/bbs/board.php?bo_table=sub1_1).

We thank the maintainers of the following projects that enable us to develop `K-Radar`:
[`OpenPCDet`](https://github.com/open-mmlab/OpenPCDet) by MMLAB.

This work was partly supported by Institute of Information & communications Technology Planning & Evaluation (IITP) grant funded by the Korea government (MSIT) (No. 01210790) and the National Research Foundation of Korea (NRF) grant funded by the Korea government (MSIT) (No. 2021R1A2C3008370).

## Citation

If you find this work is useful for your research, please consider citing:
```
@InProceedings{paek2022kradar,
  title     = {K-Radar: 4D Radar Object Detection Dataset and Benchmark for Autonomous Driving in Various Weather Conditions},
  author    = {Paek, Dong-Hee and Kong, Seung-Hyun and Wijaya, Kevin Tirta},
  booktitle = {Proceedings of the Neural Information Processing Systems (NeurIPS) Track on Datasets and Benchmarks},
  month     = {December},
  year      = {2022},
  url       = {https://github.com/kaist-avelab/K-Radar}
}
```
