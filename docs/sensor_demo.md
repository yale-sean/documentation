# Velodyne Sensor Demo

Here we will show you how to run a simple demo to demonstrate the new velodyne sensor capabilities in SEAN3.0. 

Open the `social_sim_unity` project and open the `Warehouse Scene` but do not hit Play yet.

To run a simple demo to demonstrate the new sensor capabilities navigate to `/sim_ws/tmux/sean_sensor_demo` folder to start tmuxinator

```
cd ~/sim_ws/tmux/sean_sensor_demo
tmuxinator
```

This will launch a little GUI window where you can set how many robots you want to spawn. After setting num_robots, individual robot settings should pop up in the panel where you can set any combination for the following sensors:

- `velodyne`
- `raycast`
- `camera` 

After you hit save configuration, this will save a `ros_unity_config.json` in `~\sim_ws\src\social_sim_ros\social_sim_ros\config` 

Now you can hit play on the Unity simulator, after which you should see RVIZ window appear with the velodyne, raycast, and camera topics all visualized from namespaced topics.

In subsequent runs if you want to keep the same settings, ignore the GUI window since the simulator will grab the existing `ros_unity_config.json.`



