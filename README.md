#ihmc\_valkyrie

The `ihmc_valkyrie_ros` package allows for integrating the IHMC ROS API and the NASA Johnson Space Center Valkyrie humanoid in simulation and on real robot hardware.

## Getting Started

This package provides several launch scripts. By default, they all use the latest stable release of IHMC Open Robotics Software as provided on JCenter/Bintray.

This software can also be used with a local build of IHMC Open Robotics Software. For more information, see [the GitHub Pages documentation](TODO fill this in)

##Usage

`ihmc_valkyrie_ros` provides the following launch files:

- `ihmc_valkyrie_scs.launch`: Launch an IHMC SCS simulation environment
- `valkyrie_open_humanoids_scs.launch`: Launches an IHMC SCS simulation environment designed as part of the MIT/University of Edinburgh Open Humanoids Project
- `val_diagnostic_control_robot.launch`: Launches a diagnostic controller for the physical Valkyrie robot
- `val_sliderboard_control_robot.launch`: Launches a sliderboard controller for the physical Valkyrie robot
- `val_wholebody_control_gazebo.launch`: Launches the `ihmc_ros_control` based controller for use with simulations from the `val_gazebo` package
- `val_wholebody_control_robot.launch`: Launches the `ihmc_ros_control` based controller for use with the physical Valkyrie robot


You can set the following roslaunch args:

- `use_local_build:=<true|false>`: If set to true and if you have your environment configured, this will use a local build of the IHMC software

- `ihmc_network_file:=<absolute path to network file>`: Specific the network configuration .ini file for the IHMC software. See [the GitHub pages documentation](TODO fill this in) for more information

Lastly, the SCS launch can take an argument for starting position:

- `starting_location:=<STARTING POSITION>`: Specify landmarks in the test environment to spawn the robot near.

### Starting Positions
The starting position in the demo worlds can be defined. Currently the options are:

These are the starting location options:
    DEFAULT, DRC_TRIALS_TRAINING_WALKING, DRC_TRIALS_QUALS, MID_LADDER, RAMP_BOTTOM, RAMP_TOP, NARROW_DOORWAY, BARRIERS, SMALL_PLATFORM, MEDIUM_PLATFORM,   ON_MEDIUM_PLATFORM, EASY_STEPPING_STONES, STEPPING_STONES, STAIRS, ROCKS, LADDER, IN_FRONT_OF_ZIGZAG_BLOCKS, SINGLE_CYLINDERBLOCKS, TOP_OF_SLOPES,   DEFAULT_BUT_ALMOST_PI, IN_FRONT_OF_CINDERBLOCK_FIELD, IN_FRONT_OF_TWO_HIGH_CINDERBLOCKS, IN_FRONT_OF_CYLINDER_BLOCKS, IN_FRONT_OF_SLANTED_CINDERBLOCK_FIELD,   OFFSET_ONE_METER_X_AND_Y, OFFSET_ONE_METER_X_AND_Y_ROTATED_PI, SMALL_PLATFORM_TURNED, SMALL_WALL
