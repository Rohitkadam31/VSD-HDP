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

Day 
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


Making directory 
![SKY130RTLDesignAndSynthesisWorkshops](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/33d184b1-6cae-4064-9270-e37945376abb)

Lab 2 : How to work with iverilog and GTKwave

 Step 1: Go to  design folder 

     rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files

Step 2: So there are lot of files starting with tb_

   so every file we get a assosciate file 

 Step 3: load some one from file in simulator such as 
 
         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog good_mux.v tb_good_mux.v

  Step 4: a.out file getting created 

  Step 5: Execute that file 

          rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog good_mux.v tb_good_mux.v# ./a.out

  Step 6: We get a output of simulator as a .vcd file i.e  tb_good_mux.vcd

  Step 7: Give this .vcd file with gtkwave command to simulator 

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/gtkwave tb_good_mux.vcd

  Step 8 : We get output waveform on GTkwave

   waveform on gtkwave

              
![Gtkwave-tb_good_mux vcd](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/5cd0d4c4-7e96-4b77-9b1e-cffd70337b69)


Lab 3: Checking What is Exactly into file

    rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/vim  tb_good_mux.v -o good_mux.v 

We get design and testbench 

     
![verilog files](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/c33c10b1-3b0b-4ac3-b366-854124480392)

Lab 3: Introduction to synthesizer (yosys)

Step 1: Invoke yosys 
  
    rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/yosys


step 2: yosys font will open

step 3: read the library 

      yosys> read liberty -lib../lib/sky130_fd_sc_hd_tt_025C_1v80.lib


step 4: read verilog 

      yosys> read_verilog good_mux.v


step 5: Model going to synthesis

      yosys> synth -top good_mux

step 6: generate the netlist

     yosys> abc -liberty../lib/sky130_fd_sc_hd_tt_025C_1v80.lib

abc is the command which convert our RTL into gate 


step 7: See what logic it realise 

    yosys> show 


Graphical version of logic it realise


  
![netlsit](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/1e8584dd-4cf3-47e5-addb-e15572ae4a41)


Step 8: How to write netlsit

      yosys> write_verilog good_mux_netlist.v

step 9: open it 

       yosys> !vim good_mux_netlist.v

 we get 
   
![verilog code](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/bb9e871f-21b4-4bd8-88ab-1e5d6c36f827)


Step 10: To see simplified verilog code 

    yosys> write_verilog -noattr good_mux_netlist.v

we get 



![simplified verilog](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/ce665e97-d866-4f79-aec6-b46e2d327908)


yosys> !vim good_mux_netlist .v


Flop synthesis simulation :

we are using this three files:
1)dff_asyncres.v 
2)dff_async_set.v
3)dff_asyncres_syncres.v


let's check dff_async_set.v

step 1:  

                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog dff_asyncres.v tb_dff_asyncres.v
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files#./a.out
                 
                 //we get vcd file ,copy tat file and paste 
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# gtkwave ./tb_dff_asyncres.vcd
                 
we get

when reset came it was not waiting for clock edge and immediately output went low.


![Async reset](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/70dbac0a-e13e-49df-afeb-f997335a3284)


2) Let's check dff_async_set.v
 

                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog dff_async_set.v tb_dff_async_set.v
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files#./a.out
                 
                 //we get vcd file ,copy tat file and paste 
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# gtkwave ./tb_dff_async_set.vcd


   We get

    output is going to be 1,that is the diffrence between asyncres and async_set 


  
![async set](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/383f7c09-7b9a-4c29-a5db-9ee56671c211)

3) let's check dff_syncres.v


                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog dff_syncres.v tb_dff_syncres.v
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files#./a.out
                 
                 //we get vcd file ,copy tat file and paste 
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# gtkwave  tb_dff_syncres.vcd

   we get

 both clock is high ,preference is given to sync_reset


![sync reset](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/c56ef17b-7125-4c36-aebf-e2680db807db)


Now let,s synthesis dff_asynres.v 

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys> read_verilog dff_asyncres.v
         yosys> synth -top dff_asynres
         yosys> dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show

we get


![async reset 1](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/a4f380d4-ee83-46d4-b978-d8cc6748ac9d)



Now synthesis dff_async_set.v

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys> read_verilog dff_async_set.v
         yosys> synth -top dff_async_set
         yosys> dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show


we get 


![sync set](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/b5d94d74-852d-4a32-8064-97c36e574715)

now synthesiz dff_syncres.v


         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys> read_verilog dff_syncres.v
         yosys> synth -top dff_syncres
         yosys> dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show

         
![async set async  reset](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/989938f4-f589-4a86-80af-b3b2469ba155)


DAY 3

Logic Optimization: combinational and sequential

Combinational Logic Optimisation

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog opt_check.v
         yosys> synth -top opt_check
         yosys> opt_clean -purge
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show
         
cells invoked
       ![1](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/2dddc39f-dc99-4da1-af15-efea5f286992)

 we get

![2](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/6ebe949d-d050-43f7-ac61-728a1e22b50d)

Another example

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog opt_check2.v
         yosys> synth -top opt_check2
         yosys> opt_clean -purge
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show

 cells invoked
    
![3](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/df21ed51-da6d-4d09-8a10-1643ebbb22a2)

we get


![3 1](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/01f686f1-2f1a-4b39-895b-bb08239c67cd)


         
          

   
          
       

                    








                 
                 
                  
                  









    

    









    
