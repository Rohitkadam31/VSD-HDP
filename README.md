# VSD-HDP 
VLSI Hardware Development program.

This repository contains the entire flow from the RTL design to GDSII. It covers all the steps including Synthesis (includes post-Synthesis analysis), Floorplanning, Placement, clock tree synthesis - CTS, and Routing.

Day 0: Created the Github repository

Day 1: Installation of the tools required.

First step: Installed VMBox and Ubuntu 20.04.

Hardware Requirements set as GB RAM, 70 GB HDD for the virtual machine.

Yosys Installation Flow


    $ git clone https://github.com/YosysHQ/yosys.git

    $ cd yosys

    $ sudo apt install make (If make is not installed please install it) 

    $ sudo apt-get install build-essential clang bison flex \

    libreadline-dev gawk tcl-dev libffi-dev git \
    
    graphviz xdot pkg-config python3 libboost-system-dev \
    
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
    
    $ make config-gcc

    $ make 

    $ sudo make install

invoke using yosys
![yosys](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/7c9a13e7-e7d7-4925-abdf-f5fb9b6cc3aa)

iverilog Installation Flow

       sudo apt-get install iverilog

![iverilog](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/e3a727b0-34fb-4f58-9c30-030bb62f55d0)



    
