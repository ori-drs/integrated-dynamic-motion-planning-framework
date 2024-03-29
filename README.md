Integrated Dynamic Motion Planning Framework
===================================================

## Overview
-----

This repository provides instructions on how to install our integrated framework
for predictive whole-body motion planning in dynamic environments, as described
in the paper:<br>
"Motion Planning in Dynamic Environments Using 
Context-Aware Human Trajectory Prediction", <em>Mark Nicholas Finean*, Luka Petrović*, 
Wolfgang Merkt, Ivan Marković, and Ioannis Havoutis</em>, published in Robotics and 
Autonomous Systems (DOI: 10.1016/j.robot.2023.104450). <br>

Link to: [Paper](https://doi.org/10.1016/j.robot.2023.104450)
Link to: [Preprint](http://arxiv.org/abs/2201.05058)<br>
Link to: [Video](https://www.youtube.com/watch?v=gdC3mpZNjG4&t=5s)<br>
Link to: [Dataset](https://ori-drs.github.io/oxford-indoor-human-motion-dataset/)<br>

Note: We are currently in the process of making this work publicly available. Please inform us
if you have any installation problems. We will very shortly be releasing examples to run as well.


<!-- ![alt text](framework.png) -->
<img src="framework.png" width="700">

## Install Summary
------

We list the packages required to run our framework below.

Libraries to install (consult install instructions within library):
- GTSAM ([our fork](https://github.com/ori-drs/gtsam), develop branch)
- GPMP2 ([our fork](https://github.com/ori-drs/gpmp2), release_refactoring)
- GPU-Voxels ([our fork](https://github.com/ori-drs/gpu-voxels), devel branch)
  
The following packages can be cloned and build within a catkin workspace:
- [gpu_voxels_ros](https://github.com/ori-drs/gpu_voxels_ros) (master branch)
- [sdf_mp_integration](https://github.com/ori-drs/sdf_mp_integration) (master branch)
- [genpy](https://github.com/ros/genpy) (tested with 0.6.14)
- [trajectory_prediction_ros](https://github.com/ori-drs/trajectory_prediction_ros) (master branch)
- [robot_self_filter](https://github.com/ori-drs/robot_self_filter) (ori branch)

Additionally, to perform image segmentation and human position 
estimate, you will need to run a docker image: (to be updated)
- [centermask_ros](https://github.com/ori-drs/centermask_ros) (release branch)

## Install Instructions 
-----

Prerequisites
------

- CMake >= 3.0 (Ubuntu: `sudo apt-get install cmake`)
- [Boost](http://www.boost.org/) >= 1.50 (Ubuntu: `sudo apt-get install libboost-all-dev`)

Installation (C++ libraries only)
------

- Install GTSAM (our fork).
  ```bash
  git clone https://github.com/ori-drs/gtsam.git
  cd gtsam
  git checkout develop
  mkdir build && cd build
  cmake ..
  make check  # optional, run unit tests
  make install
  ```
<!-- - Setup paths.
  ```bash
  echo 'export LD_LIBRARY_PATH=/usr/local/lib:${LD_LIBRARY_PATH}' >> ~/.bashrc
  echo 'export LD_LIBRARY_PATH=/usr/local/share:${LD_LIBRARY_PATH}' >> ~/.bashrc
  source ~/.bashrc
  ``` -->
- Install gpmp2 (our fork).
  ```bash
  git clone https://github.com/ori-drs/gpmp2.git
  cd gpmp2 && mkdir build && cd build
  cmake -DCMAKE_BUILD_TYPE=Release  ..
  make check  # optional, run unit tests
  make install
  ```
- Install GPU-Voxels (our fork).
Need to switch to g++ and gcc. Also need to download the latest eigen.
  ```bash
  git clone https://github.com/ori-drs/gpu-voxels.git
  cd gpu-voxels && git checkout devel 
  echo 'export GPU_VOXELS_INSTALL_DIR=$(pwd)' >> ~/.bashrc
  echo 'export LD_LIBRARY_PATH=$(pwd)/export/lib:$LD_LIBRARY_PATH' >> ~/.bashrc
  echo 'export GPU_VOXELS_MODEL_PATH=$(pwd)/packages/gpu_voxels_models' >> ~/.bashrc
  mkdir build && cd build
  cmake -DCMAKE_PREFIX_PATH=/{path_to_eigen_install_dir} ..
  make check  # optional, run unit tests
  make install
  ```

Catkin Workspace (C++ only)
------

  ```bash
  mkdir ws && cd ws && mkdir src && cd src
  git clone https://github.com/ori-drs/gpu_voxels_ros.git
  git clone https://github.com/ori-drs/sdf_mp_integration.git
  git clone https://github.com/ros/genpy.git
  git clone https://github.com/ori-drs/trajectory-prediction-ros.git
  git clone https://github.com/ori-drs/robot_self_filter.git
  cd ../..
  catkin build
  echo 'source /{path_to_ws}/devel/setup.bash' >> ~/.bashrc
  ```

## Citing
-----

If you use this work, please cite following publications:

```
@article{FINEAN2023104450,
title = {Motion planning in dynamic environments using context-aware human trajectory prediction},
journal = {Robotics and Autonomous Systems},
volume = {166},
pages = {104450},
year = {2023},
issn = {0921-8890},
doi = {https://doi.org/10.1016/j.robot.2023.104450},
url = {https://www.sciencedirect.com/science/article/pii/S0921889023000891},
author = {Mark Nicholas Finean and Luka Petrović and Wolfgang Merkt and Ivan Marković and Ioannis Havoutis},
}
```

## License
-----
While this repository is licensed under the BSD-3-Clause license, it uses multiple third-party packages which operate under different licenses. 

We provide a summary indication of the licenses below but please consider any licensing information 
provided in the individual packages:

| Package                               | License |
| ----------- | ----------- |
| GPU-Voxels                            | CDDL       |
| GPU-Voxels (icl_core helper library)  | CDDL        |
| GPU-Voxels (build system)             | BSD        |
| GPU-Voxels (PBA kernel code)          | BSD-like license (consult the file LICENSE_PBA.txt)        |
| GTSAM                                 | Simplified BSD        |
| GPMP2                                 | BSD        |
| robot_self_filter                     | BSD        |
| gpu_voxels_ros                        | BSD-3-Clause        |
| sdf_mp_integration                    | BSD-3-Clause        |
| trajectory-prediction-ros             | BSD-3-Clause        |
| genpy                                 | BSD        |
| centermask2                           | Attribution-NonCommercial 4.0 International        |
| centermask_ros                       | MIT        |


## Questions and Feedback
-----
We are always interested in hearing how people are using our software, 
so please get in contact if you have questions or comments about this work.
