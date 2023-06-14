# ODL-OS
This repo contains the manifest for installing the SDK and build tools required for building and running ODL build
This is a adaption of the proccess described here: https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/getting_started/installing.html


## Installing Tools
The recommended way of installing the required tools on Windows is to use Chocolatey, a package manager for Windows. Chocolatey installs the tools so that you can use them from a Windows command-line window.

To install the required tools, complete the following steps

1. [Install chocolatey.](https://chocolatey.org/install)

2. Open a cmd.exe window as Administrator. To do so, press the Windows key, type “cmd.exe”, right-click the result, and choose Run as Administrator.

3. Disable global confirmation to avoid having to confirm the installation of individual programs:

```sh
choco feature enable -n allowGlobalConfirmation
```

4. Use choco to install the required dependencies:
```sh
choco install cmake --installargs 'ADD_CMAKE_TO_PATH=System'
choco install ninja gperf git dtc-msys2 wget 7zip
```

Ensure that these dependencies are installed with their versions as specified in the Required tools table. To check the list of installed packages and their versions, run the following command:
```sh
choco list -lo
```

## Installing West
To manage the combination of repositories and versions, the nRF Connect SDK uses [Zephyr’s west.](https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/zephyr/develop/west/index.html#west)

To install west, reopen the command prompt window as an administrator to ensure that Python is initialized and selected correct version of python, and enter the following command in a command-line window:
```sh
pip install west
```

## Installing OS
Every  SDK release consists of a combination of Git repositories at different revisions. This is managed with the west.yaml file

To clone the repositories, complete the following steps:

Create a folder named ncs in your code folder. This folder will hold all SDK repositories. On the command line, go to the ncs folder (cd ncs) and initialize west with the ODL code repository.
```sh
west init -m https://github.com/Phase-1-Engineering/ODL-OS.git --mr main
```
This will clone the manifest repository into nrf.

Enter the following command to clone the project repositories:

```sh
west update
```

Depending on your connection, this might take some time.

Export a Zephyr CMake package. This allows CMake to automatically load the boilerplate code required for building SDK applications:

```sh
west zephyr-export
```

## Install additional Python dependencies

The SDK requires additional Python packages to be installed.

Use the following commands to install the requirements for each repository. This might take some time

```sh
pip3 install -r zephyr/scripts/requirements.txt
pip3 install -r nrf/scripts/requirements.txt
pip3 install -r bootloader/mcuboot/scripts/requirements.txt
```

## Install the Zephyr SDK

The Zephyr Software Development Kit (SDK) contains toolchains for each of Zephyr’s supported architectures. Each toolchain provides a compiler, assembler, linker, and some, but not all, of the rest of the programs required to build Zephyr applications. The Zephyr SDK also includes additional host tools, such as custom QEMU and OpenOCD builds. It is at the base of the nRF toolchain, which adds on top of it several tools and modules of its own.

1. Open a cmd.exe window by pressing the Windows key typing “cmd.exe”.

2. Download the latest Zephyr SDK bundle to your program files repo:
```sh
cd %PROGRAMFILES%
wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.16.0/zephyr-sdk-0.16.0_windows-x86_64.7z
```
3. Extract the Zephyr SDK bundle archive:
```sh
7z x zephyr-sdk-0.16.0_windows-x86_64.7z
```

4. Run the Zephyr SDK bundle setup script:
```sh
cd zephyr-sdk-0.16.0
setup.cmd
```
