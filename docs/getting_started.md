## Setup

This guide will walk you through setting up the simulation environment where Unity runs in Windows and ROS runs in a WSL2 virtual machine.

### Dependencies

- Confirm that your system is running Windows 10 or Windows 11.

- Install [WSL](https://learn.microsoft.com/en-us/windows/wsl/install).

  - If you already have WSL installed, make sure it is running WSL 2. In PowerShell, set WSL 2 as the default version for newly installed Linux distributions: `wsl.exe --set-default-version 2`

- Download and install [Ubuntu 20.04.06 LTS](https://apps.microsoft.com/detail/9mttcl66cpxj?hl=en-US&gl=US).

  - In PowerShell, set the default Linux distribution that WSL commands will use to be Ubuntu 20.04: `wsl.exe --set-default Ubuntu-20.04`

- Download and install [Git](https://git-scm.com/install/windows).

### Install Unity

> **Note**: Install Unity in Windows, not in WSL2.

- Download and install [Unity Hub](https://unity.com/download).

- Log in to Unity Hub. If you do not have an account, create a Unity account now.

### Checkout & Open the SEAN 3.0 Unity Project

- Clone the [`social_sim_unity`](https://github.com/yale-img/social_sim_unity) into some Unity Project folder

- Checkout the **hdrp-rl** branch: `git checkout hdrp-rl`

- Initialize and update all submodules in the repository: `git submodule update --init --recursive`

  > **Note**: If you run into errors such as:
  > ```text
  > error: inflate: data stream error (incorrect data check)
  > error: unable to read sha1 file of <path/to/asset/file>
  > ```
  > Add the `--force` flag to this command:
  >```text
  > git submodule update --init --recursive --force
  >```

- Launch Unity Hub and open the cloned `social_sim_unity` project

  - If the required Unity Editor version is not installed, Unity Hub will prompt you to install it when opening the Sean 3.0 project.

  - For more details, see the Unity documentation on [adding an existing project from disk](https://docs.unity3d.com/hub/manual/AddProject.html#add-an-existing-project-from-your-disk) and [opening a project with a different Editor version](https://docs.unity3d.com/hub/manual/OpenProject.html#open-with-a-different-editor-version).  

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