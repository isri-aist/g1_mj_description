# g1_mj_description

This repository contains the G1 robot model for [mc_mujoco](https://github.com/rohanpsingh/mc_mujoco).

The package will install the files in this directory so that mc_mujoco can pick them up automatically.

Please note that **G1_23dof** (default) and **G1_29dof** variants are supported.

## Requirement 

Please make sure [mc_mujoco](https://github.com/rohanpsingh/mc_mujoco) is installed.

## Install

### From source

In order to install from source please run the following commands:

```bash
git clone https://github.com/isri-aist/g1_mj_description
cd g1_mj_description
mkdir build && cd build
cmake ..
make install
```

## To run

Your mc_rtc configuration file (typically ~/.config/mc_rtc/mc_rtc.yaml) should contain the following lines:

```yaml
# General mc_rtc configuration to run a G1 controller
MainRobot: G1  # Or G1_23dof, G1_29dof (G1 defaults to 23-DOF variant)
Enabled: Posture  # Edit with your controller
Timestep: 0.001
```

Then run mc_mujoco:

```bash
mc_mujoco
```

## CMake options

- `SRC_MODE` if `ON` the files loaded by mujoco will point to the source rather than the installed files (default `OFF`)

## Supported models

- **g1_23dof**: G1 robot with 23 degrees of freedom (base configuration)
- **g1_29dof**: G1 robot with 29 degrees of freedom (includes additional waist and wrist joints)
