HOWTO
====================

### Environment Setup
Create a workspace for uEmu-Ratava project in home directory. Then add the workspace into bash profile (e.g., ```~/.bashrc```).
```sh
mkdir -p ${HOME}/uEmu
export uEmuDIR=${HOME}/uEmu
```
This repository contains the ``repo`` manifests to manage S2E-uEmu's repositories.

```sh
sudo apt-get install git-repo
cd $uEmuDIR
repo init -u https://github.com/MCUSec/manifest.git -b ratava
repo sync
```
Build & Install
```sh
cd $uEmuDIR/scripts
./build.sh
```

### RatavaDump 

This section shows how to use ```RatavaDump``` plugin to trace the execution of the ```hello world``` sample program.

##### Configuration

The following configurations should be done prior to run ```RatavaDump```. Open ```$uEmuDIR/uEmu-config.lua``` file by ```vim```.

In ```pluginsConfig.RatavaDump``` structure:
- Specify the output path of tracing log in ```outputTrachPath``` field.
- Sepcify the end point in which switch to other exploration paths in ```traceEndPoint``` field. (Default is ```0x5f6``` for ```hello world``` program)

In ```pluginsConfig.Vmi``` structure:
- Specify the path of VMI base dirs in ```baseDirs``` field.

##### Run

Run ```DumpRatava```: 
```sh
$uEmuDIR/launch-uEmu.sh debug
```
Then, press ```r``` in ```gdb``` console to start. Once the execution terminated, please find the tracing log in the output path.

##### Source Code
Source code of ```RatavaDump``` is located in ```$uEmuDIR/s2e-ratava/libs2eplugins/src/s2e/Plugins/RatavaDump```.

To rebuild it, please run:
```sh
cd $uEmuDIR/build/libs2e-release/arm-s2e-softmmu
make
```

