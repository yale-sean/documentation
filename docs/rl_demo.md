# Reinforcement Learning Demo


Here we will show you how to run a simple learning demo to train a reinforcement learning policy using SEAN 3.0 with multiple agents.

Open the `social_sim_unity` project and open the `Warehouse Scene` but do not hit Play yet.

To run a simple demo to demonstrate the new sensor capabilities navigate to `/sim_ws/tmux/multi_agent_sean` folder to start tmuxinator

```
cd ~/sim_ws/tmux/multi_agent_sean
tmuxinator
```

### The `.tmuxinator.yml` launches the following files

* `rosrun social_sim_ros map_publisher.py` 
    * Note: this launches the map_publisher, it is MANUALLY SET to warehouse for testing purposes so be sure to only use Unity warehouse scene
* `rosrun social_sim_ros multi_agent_tcp_server.py`
    * Note: this starts the ROS tcp server for registering all publishers, transforms, services, and publishers with Unity. When this is launched, it expects a `ros_unity_config.json` file in the `social_sim_ros\social_sim_ros\src` folder which is automatically created as soon as you hit save config in the sean interface gui. This runs on port 10000.
* `rosrun rviz rviz -d $(rospack find social_sim_ros)/config/multi_agent.rviz    `
    * Note: this launches a custom rviz config, currently hardcoded to two agents to visualize pointclouds, TF, and laserscans
* `python3 $(rospack find social_sim_ros)/src/sean_interface.py` 
    * Note: this launches the sean_interface gui where you should specify how many robots you want, what types, and what sensors. Also, you can enable synchronous mode and tick duration here. 
* `conda activate marl && cd $HOME/sim_ws/src/social_sim_multiagent && sleep 5 && python3 maddpg-pytorch/main.py a`
    * This is the openaigym-ros interface which instantiates a synchronous tcp server whenever sync mode is true. client.tick() must be called before env.reset() and env.step(). If there are no messages that say Odom received and Scan received in this window, it is likely that unity did not initialize all agents and topics before the first tick message was sent. Adjust sleep as necessary.
* `sleep 5 && rosrun social_sim_ros plot_robot_trajectory.py`
    * This just visualizes path markers for the `/robot/i/cmd_vel` topics in rviz so you can track the path of the RL policy. 

### Some Tips:

The topics for each robot are prefixed `/robot/{i}/` and the frames are prefixed `robot_{i}_` 

Synchronous mode allows you to pause and unpause the ROSClock that is publishing in Unity. Unity will perform physics fixed updates as much as possible before tick_duration elapses in unity simulation time. To control the fixed timestepping of the Unity environment you need to run client.tick() imported from synchronous_tcp_server (SychronousTcpServer class). 

* Note: When the simulation is paused in synchronous mode, unity will not receive or publish any messages. The sychronous tcp server runs on port 8080 so make sure that port forwarding rules are enabled for 8080.

If you want to reset the agent initialization settings, note that the sean_interface gui resets parameters FOR THE NEXT RUN unless there is no config json available at which the multi_agent_tcp_server.py will hang and complain that no such file is available. If this is the case, you should generate configuration, close the tmux terminal, relaunch tmuxinator, then hit play in Unity.

The order of execution should always be:

1. If `ros_unity_config.json` is present: then

```
cd ~/sim_ws/tmux/multi_agent_sean
tmuxinator
```

1. Hit play in Unity, at which point you should see initialization messages in Unity console. 
2. If you want to change the configuration for the next run, save config in SEAN Configurator GUI and `tmux kill-session` and unclick Play in Unity, then return to step 1.