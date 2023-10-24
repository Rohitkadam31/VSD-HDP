# VSD-HDP 
VLSI Hardware Development program.

This repository contains the entire flow from the RTL design to GDSII. It covers all the steps including Synthesis (includes post-Synthesis analysis), Floorplanning, Placement, clock tree synthesis - CTS, and Routing.

Day 0: Created the Github repository

Day 1: Installation of the tools required. 

First step: Installed VMBox and Ubuntu 20.04.

Hardware Requirements set as 6 GB RAM, 70 GB HDD for the virtual machine.

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

Gtkwave installation

        sudo apt update
        sudo apt install gtkwave

![gtkwave](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/eb9ab7f3-be17-4502-8072-97df47b21e2c)

Day 3
RTL design using verilog with SKY130 technology

 1 : Environment setup for running the other labs
 

 step 1 :Make a directory VLSI
 
 step 2: Gitclonning
 
 then go to 
      
       https://github.com/kunalg123

  then go to github page for our workshop 

       https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop

and copy the code link from there 

         https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git

and paste to gitclone and then if you hit the enter this will create this directory  

       sky130RTLDesignAndSynthesisWorkshops

      
       
       ![SKY130RTLDesignAndSynthesisWorkshops](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/8d49b3aa-42f3-4960-be08-d8c63c089ed4)


     
       





    
