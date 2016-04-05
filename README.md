#ihmc\_valkyrie\_ros

The `ihmc_valkyrie_ros` package allows for integrating the IHMC ROS API and the NASA Johnson Space Center Valkyrie humanoid in simulation and on real robot hardware.

## Getting Started

This package provides several launch scripts. By default, they all use the latest stable release of IHMC Open Robotics Software as provided on JCenter/Bintray.

This software can also be used with a local build of IHMC Open Robotics Software. For more information, see [the IHMC ROS Java Adapter](https://github.com/ihmcrobotics/ihmc_ros_core/tree/develop/ihmc_ros_java_adapter).

##Usage

`ihmc_valkyrie_ros` provides the following launch files:

- `ihmc_valkyrie_scs.launch`: Launch an IHMC SCS simulation environment
- `valkyrie_open_humanoids_scs.launch`: Launches an IHMC SCS simulation environment designed as part of the MIT/University of Edinburgh Open Humanoids Project
- `val_diagnostic_control_robot.launch`: Launches a diagnostic controller for the physical Valkyrie robot
- `val_sliderboard_control_robot.launch`: Launches a sliderboard controller for the physical Valkyrie robot
- `val_wholebody_control_gazebo.launch`: Launches the `ihmc_ros_control` based controller for use with simulations from the `val_gazebo` package
- `val_wholebody_control_robot.launch`: Launches the `ihmc_ros_control` based controller for use with the physical Valkyrie robot

### Using val_wholebody_control_\* launch files

Some configuration must be done to use the IHMC whole-body control algorithm in the Valkyrie package. At the time of this writing, the whole-body control launch files are not integrated with Bintray or the `ihmc_ros_java_adapter`. You will need to do the following on the computer where the controller will be run:

- Configuring security limits for starting realtime threads. Edit `/etc/security/limits.conf` and add the following (replacing [username] with your local user name):
```
[username]       soft    cpu     unlimited
[username]       -       rtprio  100
[username]       -       nice    40
[username]       -       memlock unlimited
```

- Set up your IHMC IP Addresses. See [The Network Parameters documentation](https://github.com/ihmcrobotics/ihmc_ros_core/blob/develop/ihmc_ros_common/IHMCNetworking.md) for more information. Note that the wholebody launchers ***do not*** currently use the config files in the `configurations` directory. They use a configuration common to the IHMC field deployments, which is `$HOME/.ihmc/IHMCNetworkParameters.ini`. You can also use environment variables as described in the documentation. The bare minimum you will need is a `logger`/`IHMC_LOGGER_IP` set.

- You must have a local clone of [IHMC Open Robotics Software](https://github.com/ihmcrobotics/ihmc-open-robotics-software) and you must "deploy" to the computer that will be running the controller. This can be accomplished via Gradle tasks. For example, to deploy locally for usage w/ Gazebo you use the `deployLocal` task, and for pushing code on to a Valkyrie robot you can use the `deploy` task.

Local deploy example:
```bash
$ cd <code clone location>
$ ./gradlew :Valkyrie:deployLocal
```

For the physical robot `deploy` task (`./gradlew :Valkyrie:deploy`), you will need to configure a few Gradle properties. Create/edit the file `$HOME/.gradle/gradle.properties` and set the following values:

```properties
#ip address of your Link computer
valkyrie_link_ip=

#ip address of your Zelda computer
valkyrie_zelda_ip=

#SSH username for the Valkyrie onboard computers:
valkyrie_realtime_username=

#SSH password for the Valkyrie onboard computers:
valkyrie_realtime_password=
```

### Other launch files

You can set the following roslaunch args:

- `use_local_build:=<true|false>`: If set to true and if you have your environment configured, this will use a local build of the IHMC software

- `ihmc_network_file:=<absolute path to network file>`: Specific the network configuration .ini file for the IHMC software. See [the GitHub pages documentation](TODO fill this in) for more information

Lastly, the SCS launch can take an argument for starting position:

- `starting_location:=<STARTING POSITION>`: Specify landmarks in the test environment to spawn the robot near.

### Starting Positions
The starting position in the demo worlds can be defined. Currently the options are:

These are the starting location options:
    DEFAULT, DRC_TRIALS_TRAINING_WALKING, DRC_TRIALS_QUALS, MID_LADDER, RAMP_BOTTOM, RAMP_TOP, NARROW_DOORWAY, BARRIERS, SMALL_PLATFORM, MEDIUM_PLATFORM,   ON_MEDIUM_PLATFORM, EASY_STEPPING_STONES, STEPPING_STONES, STAIRS, ROCKS, LADDER, IN_FRONT_OF_ZIGZAG_BLOCKS, SINGLE_CYLINDERBLOCKS, TOP_OF_SLOPES,   DEFAULT_BUT_ALMOST_PI, IN_FRONT_OF_CINDERBLOCK_FIELD, IN_FRONT_OF_TWO_HIGH_CINDERBLOCKS, IN_FRONT_OF_CYLINDER_BLOCKS, IN_FRONT_OF_SLANTED_CINDERBLOCK_FIELD,   OFFSET_ONE_METER_X_AND_Y, OFFSET_ONE_METER_X_AND_Y_ROTATED_PI, SMALL_PLATFORM_TURNED, SMALL_WALL
