<div align="center">
<img src="./assets/img/Carla Truck Trailer.png" width=100% style="vertical-align: bottom;">
<h2>Carla Truck Trailer: Simulation truck trailer system in a more realistic way</h2>

[**Komasa Qi**](https://github.com/KomasaQi), School of Vehicle and Mobility, Tsinghua University
<div align="center">
  <img src="https://img.shields.io/badge/Carla Version-0.9.13-blue.svg" alt="Project Badge">
  <img src="https://img.shields.io/badge/UnrealEngine-4.26-green.svg" alt="Duration Badge">
  <img src="https://img.shields.io/badge/Status-Under Construction-orange.svg" alt="Status Badge">
</div>
</div>

Implementation facilitatiing creation of a realistic truck trailer system, including sensor simulations of camera and lidar as well as other carla supported sensor forms. Also, we include calibration board assets for camera-lidar system and camera inner parameter calibration.

<div style="display: flex; justify-content: center; align-items: center; gap: 2%;">

  <img src="./assets/gif/truck_moving.gif" width="52%" alt="Video 1">

  <img src="./assets/gif/attachment.gif" width="45%" alt="Video 2">

</div>

## Getting Start
First download the project, and then copy the corresponding files into your `carla installation folder` and your `carla-ros-bridge installation folder`. If there are files with the same name, if the files you haven't modified, then just substitute the files into your folder. The installation finishes as soon as the files are copied to the correct position. If you haven't started carla, please refer to The [installation instruction file](https://github.com/KomasaQi/HitchOpen-THICV-Stack/tree/main/tutorial/install_carla).

Typically, parent folder of `CARLA_ROOT` is the user folder, and so do the carla-ros-bridge.

**First you start a scene**, such as `Town10HD_Opt`, and then if you want to control the trailer without ROS, you can initiate a new terminal, and 
``` bash
    cd $(CARLA_ROOT)/PythonAPI/examples
    python3 manual_control.py --filter scania_truck

```
If you want to run with full ROS sensors and control channels available, run as
``` bash
    roslaunch carla_ros_bridge carla_ros_bridge_with_scania_truck.launch
```
This opens the predefiend rviz interface shows the sensor raw data directly. To control the vehicle, you still need to use the interface that pumps out with vehicle data. Press `B` to toggle manual control command, then you can control with `WASD` and `Q` to toggle reverse, `Space` to activate hand brake temporally.


After running the code, if you `ctrl+c` the roslaunch, you may find that the world of carla getting stuck. To recover control, you can run the code in another terminal:
``` bash
    python3 # open python environment
```
in the python environment
``` python
    import carla
    client = carla.Client('localhost',2000)
    client.set_timeout(5.0) 
    client.reload_world()
    exit()
```
Then the world gets reloaded and you regain the control. You can then stop the simulation on the UE Editor.


## Practice your driving skill
This project was originated from an open source game: Truck Trailer Simulator implemented in the platform of Unreal Engine 4. You can Explore the game in the way demonstrated below to get familiar with the models and the way to manipulate trailer. 

<div style="display: flex; justify-content: center; align-items: center; gap: 2%;">

  <img src="./assets/gif/game_original.gif" width="48%" alt="Video 1">

  <img src="./assets/gif/box_trailer_run.gif" width="48%" alt="Video 2">

</div>

After starting carla, usually by the codes bellow, you can then open the folder: `TruckTrailer`

``` bash
cd carla # path to your $(CARLA_ROOT)
make launch # or other way you open the carlaUE4 editor 
```
and you can double click to open the `level` file, which opens the game. Then click the `Start` button and the simulation starts. You can play around in this environment. In this game (no in carla), to attach to either of the trailers, you can drive reversely below the trailer just like what you do in reality. Then the text `"Press 'T' to Attach"` shows on the main window of UE editor.

After pressing `T`, you attach to the trailer and the camera view changes to a longer distance.

## Calibration Assets
In addtition to the truck trailer system, we also included some assets you can put in Carla to calibrate camera and camera-lidar system.
<div style="display: flex; justify-content: center; align-items: center; gap: 2%;">

  <img src="./assets/gif/calib_boards.gif" width="48%" alt="Video 1">

  <img src="./assets/gif/place_boards.gif" width="48%" alt="Video 2">

</div>

The `hole calib board` is suitable for [Fast_Calib](https://github.com/hku-mars/FAST-Calib) and the `checkboard` with each grid **5 cm** 8x7 crosses is suitable for `camera_calibration` official package native to ROS. 


## About

This project belongs to THICV (Tsinghua University Intelligent & Connected Vehicle Research Group) and is open source, we holp this facilitates all researchers that need to simulate truck-trailer system in a more realistic environment espesially including the closed-loop simulation of sensors. Since ROS is a very open platform and has a lot of excellent algorithms contributed by the developers around the world, we choose to implement the simulation system on Carla which connect seamlessly with ROS. 

If this helps your research, please cite this project as
``` latex
@online{CarlaTruckTrailer,
  author = {KomasaQi},
  title = {Carla-Truck-Trailer},
  url = {https://github.com/KomasaQi/Carla-Truck-Trailer},
  urldate = {[date-you-download]}
}
```