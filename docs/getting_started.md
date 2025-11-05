### Install Unity

- Important: Install Unity in Windows, not in WSL2.

- Download and install the [UnityHub](https://unity.com/download).

  - Download and install UnityHub from: [https://unity3d.com/get-unity/download](https://unity3d.com/get-unity/download)

  - Login to UnityHub. If you do not have an account create a Unity account now.

### Checkout the SEAN3 Unity Project code

Clone the following repo into some Unity Project folder

```
https://github.com/yale-img/social_sim_unity
```

Make sure you are on **hdrp-rl** branch

```
git checkout -b hdrp-rl
```

Now, since this repo has several submodules run

```
git submodule update --init --recursive
```

Run the project in Unity Hub by clicking on the project name: `social_sim_unity`, you may be prompted to install the correct version of Unity. Be sure to install the correct version of Unity which should be 6000.0.47f1

## WSL side with ROS noetic

### Install ROS and Use Preconfigured Workspace.

Install by following the ROS Noetic Setup Guide. If you run into any problem or want to learn more about ROS Noetic, see ROS Noetic. Then, you can use the sim_ws as a starting point for your catkin workspace. Start by checking out the repository.

**Install preconfigured workspace**

```
git clone https://github.com/yale-img/sim_ws ~/sim_ws
```

**Then, run the installer scripts to install all required packages:**

```
cd ~/sim_ws/
./scripts/setup.sh
```

**In your base environment, install custom tkinter for the GUI interface**

```
pip install customtkinter
```

* Ensure that both your `~/sim_ws` and `roscd social_sim_ros` git branches are on `hdrp-rl`

**Open-AI Gym Setup**

Install `uv`:
https://docs.astral.sh/uv/getting-started/installation/#standalone-installer

Navigate to the `social_sim_multiagent` repo

```
cd ~/sim_ws/src/social_sim_multiagent
```

and run the following commands to install all the required dependencies for the learning features

```
uv sync
uv pip install -e multi-agent-envs/
```