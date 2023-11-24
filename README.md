 # VSD-HDP 
VLSI Hardware Development program.

This repository contains the entire flow from the RTL design to GDSII. It covers all the steps including Synthesis (includes post-Synthesis analysis), Floorplanning, Placement, clock tree synthesis - CTS, and Routing.

Day 0: Created the Github repository

Day 1: Installation of the tools required. 

First step: Installed VMBox and Ubuntu 20.04.

Hardware Requirements set as 6 GB RAM, 70 GB HDD for the virtual machine.

# Yosys Installation Flow


    $ git clone https://github.com/YosysHQ/yosys.git

    $ cd yosys

    $ sudo apt install make (If make is not installed , install it) 

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
# RTL design using verilog with SKY130 technology

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


# Flop synthesis simulation :

we are using this three files:
1)dff_asyncres.v 
2)dff_async_set.v
3)dff_asyncres_syncres.v


* let's check dff_async_set.v

step 1:  

                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog dff_asyncres.v tb_dff_asyncres.v
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files#./a.out
                 
                 //we get vcd file ,copy tat file and paste 
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# gtkwave ./tb_dff_asyncres.vcd
                 
we get

when reset came it was not waiting for clock edge and immediately output went low.


![Async reset](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/70dbac0a-e13e-49df-afeb-f997335a3284)



 * Let's check dff_async_set.v
 

                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files/iverilog dff_async_set.v tb_dff_async_set.v
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files#./a.out
                 
                 //we get vcd file ,copy tat file and paste 
                 
                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# gtkwave ./tb_dff_async_set.vcd


   We get

    output is going to be 1,that is the diffrence between asyncres and async_set 


  
![async set](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/383f7c09-7b9a-4c29-a5db-9ee56671c211)

* let's check dff_syncres.v


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


# DAY 3

# Logic Optimization: combinational and sequential

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


Sequential Logic Optimisation

 dff_const1: 

    
         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog dff_const1.v
         yosys> synth -top dff_const1
         yosys> dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show

  
cells invoked 

  
![4](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/52513936-5470-401a-9a65-8a8c6f58e066)


we get

![4 2](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/b9fe6734-c60d-4e02-b4ff-e8e8fe9a9011)



Another example

Dff_const2:


         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog dff_const2.v
         yosys> synth -top dff_const2
         yosys> dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show


cells invoked 

![1 (1)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/8943f56c-adc5-4b6e-ac1e-0fbfe22b1574)


we get

![1 (2)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/d89920b3-10e7-47c3-92f4-2eba71badc5b)


Unused output optimization : 

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog counter_opt.v
         yosys> synth -top counter_opt
         yosys> dfflibmap -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show


Cells invoked 

![1 (2)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/5a299ed2-a8e4-4d13-a856-0242457b4ff2)


we get 

![1 (1)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/78206dae-d6e7-4e10-a065-b72b115ef0d3)


If we modify the RTL we see following changes

   
![2 (1)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/105f7004-5ed1-46c4-b56c-a7d5bdb6e74a)

three flops are added (infered).


After Change in RTL we get

![2 (2)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/76fafcdb-f956-4931-8b77-c671ee9b2c87)


# DAY 4:

# GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

# GLS : Gate level simulation

GLS using IVERILOG


![3](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/7f926246-d81f-43fb-87a2-19a121d7f288)


# How to invoke GLS 

Requirement:
              1)Netlist
              2) verilog models of standard cell libraries
              3) Testbench 


Process :

we have to  submit this three to iverilog ,iverilog dump out the vcd file and we get waveform on gtkwave


Step 1:

                 rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# gtkwave tb_ternary_operater_mux.vcd

  we get


![Screenshot 2023-11-03 175929](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/a39a90a6-68ba-4791-9f02-8ef79c970b58)

Now synthesise this 

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog ternary_operater_mux.v
         yosys> synth -top ternary_operater_mux
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> write_verilog -noattr ternary_operater_mux_net.v
         yosys>show


 We get 

 
![Screenshot (1)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/5721da9a-5639-4b91-ad17-3ca45d29ecfd)


Bad_Mux:

    rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog file# iverilog bad_mux.v tb_bad_mux.v
    rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog file# ./a.out

    //we get vcd file,give it to gtkwave
    rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog file# gtkwave  tb_bad_mux.vcd

we get

![Screenshot (3)](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/842189e0-4dfe-4968-bb48-e7ef7d0a5fa1)


we can see it is not working like mux.

Now synthesis this :

         
         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog bad_mux.v
         yosys> synth -top bad_mux
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> write_verilog -noattr bad_mux_net.v
         
simulate bad_mux netlist

          
         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files # iverilog ../lib/verilog_model/primitives.v ../lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v
     rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files # ./a.out
      rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files # gtkwave tb_bad_mux.vcd

We get

![Screenshot 2023-11-03 190204](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/46265b2b-2756-43ef-a452-d7e74c3340bb)


Synthesis simulation mismatch using blocking caveat:

           
             rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog file# iverilog blocking_cavet.v tb_blocking_cavet.v
             rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog file# ./a.out

             //we get vcd file,give it to gtkwave
              rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog file# gtkwave  tb_blocking_cavet.vcd


we get
 
   ![55](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/1fe380db-4a40-4a86-b6bd-170ad9bf45fe)


now synthesis:

         rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files# yosys
         yosys>read_liberty -lib ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> read_verilog blocking_caveat.v
         yosys> synth -top blocking_caveat
         yosys> abc -liberty ../lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> write_verilog -noattr blocking_caveat_net.v
         yosys>show



we get

   ![6](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/5b56c28b-ef12-4fb3-9844-707d19f9d229)


Gtkwave:

        rohit@rohit-VirtualBox:~/sky130RTLDesignAndSynthesisWorkshop/verilog files # iverilog ../lib/verilog_model/primitives.v ../lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat.v 
        tb_blocking_caveat.v


  we get

  ![Screenshot 2023-11-03 195924](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/0f1dbf14-c529-4e7a-9d47-b5baecb33f40)


  # iiitb_r2_4bit_bm -> Radix-2 4-Bit Booth's Multiplier     

### Description 
 This project simulates the Radix-2 4-Bit Booth's Multiplier using Verilog HDL. It can be used to multiply two 4-bit binary signed number in a efficient manner with 
 less number of addition operation.
 
## Introduction
Booth's Multiplier is based on Booth's Multiplication Algorithm. It proposes an efficient way for multiplying two signed integers in there 2's complement form such that the number of partial products is reduced which ultimately lead to the reduction of number of addition operation required for generating the final result.


## Application 
Applications of Booth’s Multiplier

•	They can be used as a fundamental unit for MAC block.<br>
•	They can be used in filters like FIR and IIR.<br>
•	They can be used in Processing Element of Systolic Array

## Block Diagram 

![Circuit_crop](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/def99784-b204-440e-b602-2637a2249183)<br>As shown in the Block Diagram, Q and M are 4-bit registers that stores the multiplier and multiplicand respectively. It also consist of a 4-bit arthematic unit capable of performing both addition and subtractions. A MOD-4 counter is also present in order to keep track of shifting operation. A and Q are 4-bit shift register. The product is produced in 8_bit register P.<br>
## Working
The multiplication operation through Booth’s algorithm is efficient compared to traditional shift and multiplication process because it produces the result with lesser addition operation.

![Flowchart_crop](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/79d0463c-c8f6-4547-b9ee-3ebf2c93b35d)
<br>
The above figure shows the flowchart of Booth’s Algorithm. At every clock cycle the two bits (Q0 , Q-1) are inspected for determination of operation .The Q0 refers to Q[0]. If the (Q0 , Q-1) are same (1,1) 0r (0,0) then only right shift operation is performed. If the (Q0 , Q-1) are same (1,0) then subtraction (A-M) followed by right shift is performed. If the (Q0 , Q-1) are same (0,1) then addition (A+M) followed by right shift operation is performed. This cycle is repeated as many times as the specified bits of Booth’s Multiplier is given. This selectivity in performing addition /subtraction operation enables it to produce result efficiently.

* Some Youtube links of working:
  
https://youtube.com/shorts/Ee2VT0C-TUA?si=oTUdyXXB6IwUgPz4

https://youtu.be/DIp4GqSCZho?si=V4mQl17c-KJKyJPn

* RTL Simulation (Pre-synthesis) :

       rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ iverilog iiitb_r2_4bit_bm.v iiitb_r2_4bit_bm_tb.v
  //a.out created
  
       rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ ./a.out
  
   //  we get vcd file
  
  ![2 (1)](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/be72276a-4e7f-4ad6-b6c5-9a9fecc9176e)

       rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ Gtkwave design.vcd

  We get RTL Simulation i.e Pre-synthesis Simulation

  ![2 (2)](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/2ee1f4ac-2f47-4720-9e18-57ba6fcfa791)




## Synthesis :

The synthesis in the OpenLane flow is carried out by yosys.

* RTL to synthesize : iiitb_r2_4bit_bm.v

* RTL Code :

 
           module iiitb_r2_4bit_bm(
           input clk,
          	input load,
          	input reset,
	          //inputs
           input [3:0] M,
	          input [3:0] Q,
	
          	//outputs
          	output reg [7:0] P

           );
	 
	          reg [3:0] A 		=  4'b0;
         	 reg Q_minus_one 	=  0;
	          reg [3:0] Q_temp 	=  4'b0;
         	 reg [3:0] M_temp 	=  4'b0;
	          reg [2:0] Count 	=  3'd4;
	 
	 
	 
        	 always @ (posedge clk)
        	 begin
	        	if (reset == 1)
		begin
			A 			 =  4'b0;		//reset values
			Q_minus_one  =  0;
			P 			 =  8'b0;
			Q_temp 		 =  4'b0;
			M_temp 		 =  4'b0;
			Count 		 =  3'd4;

		end

		else if (load == 1)
		begin
			Q_temp 		=  Q;
			M_temp 		=  M;
		end

		else if((Q_temp[0] == Q_minus_one ) && (Count > 3'd0))
		begin
			Q_minus_one =  Q_temp[0];
			Q_temp 		=  {A[0],Q_temp[3:1]};				// right shift Q							
			A 			=  {A[3],A[3:1]};					// right shift A	
		    Count 		=  Count - 1'b1;					
		end
		else if((Q_temp[0] == 0 && Q_minus_one == 1)  && (Count > 3'd0))
		begin
			A 			=  A + M_temp;
			Q_minus_one =  Q_temp[0];
			Q_temp 		=  {A[0],Q_temp[3:1]};				// right shift Q
			A 			=  {A[3],A[3:1]};					// right shift A
			Count 		=  Count - 1'b1;
		end
		else if((Q_temp[0] == 1 && Q_minus_one == 0)  && (Count > 3'd0))
		begin
			A 			=  A - M_temp;
			Q_minus_one =  Q_temp[0];
			Q_temp 		=  {A[0],Q_temp[3:1]};				// right shift Q
			A 			=  {A[3],A[3:1]};					// right shift A
			 Count 		=  Count - 1'b1;
		end
		else 
		begin
			Count = 3'b0;
		end
		P = {A, Q_temp};
		
	         end

          endmodule

* process to synthesize iiitb_r2_4bit_bm on yosys :

         rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ yosys
         yosys> read_verilog iiitb_r2_4bit_bm.v
         yosys> synth -top iiitb_r2_4bit_bm
         yosys> dfflibmap -liberty ../iiitb_r2_4bit_bm/lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys> abc -liberty ../iiitb_r2_4bit_bm/lib/sky130_fd_sc_hd_tt_025C_1v80.lib
         yosys>show

 * cells invoked :
      
![1 (1)](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/1489c3e3-671c-48ce-b587-b69888e5e8ac)


* RTL Synthesis :
  
![1 (2)](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/6e4fb193-df5f-4b0c-be2c-cd456e2082d1)


# Gate Level Simulation (GLS)

(post-synthesis)

         rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ iverikog /home/rohit/vsdflow/iiitb_r2_4bit_bm/verilog_model/primitives.v 
        /home/rohit/vsdflow/iiitb_r2_4bit_bm/verilog_model/sky130_fd_sc_hd.v iiitb_r2_4bit_bm_synth.v iiitb_r2_4bit_bm_tb.v
 //we get a.out file
 //execute it
 
	      rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ ./a.out

 //we get dumpfile (vcd file) for output
 
![3 (1)](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/61a55b53-dbcc-4913-af10-bf8942cd2e1c)

// copy that vcd file and give it to gtkwave for simulation
          
	  rohit@rohit-VirtualBox:~/vsdflow/verilog/iiitb_r2_4bit_bm $ gtkwave design.vcd
   
 we get Gate level simulation 

![3 (2)](https://github.com/Rohitkadam31/iiitb_r2_4bit_bm-Rohit/assets/148602919/4195fa2f-48e8-4ef9-b2b1-2fe31932e04c)

We can see that GLS simulation matching to RTL simulation 

# STA -Static Timing Analysis

Delay : 
delay is function of load capaticance. 

Max and minimum delay constraint  

Max delay :
Maximum time the combinational circuit can be taken including the setup time is called Max delay constraint . 

Min delay constraint :

The data path is so short that it passes through. several registers during the same clock cycle  

If we have fast current source we get less delay.   

#  Constraints: 
Constraints are the instructions that the designer apply during various step in VLSI chip implementation, such as logic synthesis, clock tree synthesis, Place and Route, and  Static  Timing Analysis. 

* Advance synthesis and STA using design compiler constraints.


# Introduction to STA

Delay is a function of input transition i.e current (inflow) and output load i.e load capacitance (size of the bucket). [ direct proportional ]

Timing arc --> delay infromation from all inputs to all outputs eg 2 i/p AND gate has 2 timing arcs -> a-q and b-q. Any changes in the inputs will affect the output. For a D FF we have 3 timimg arcs -> Clk - Q delay , setup time and hold time. For a D latch we have 4 timing arcs - D - Q delay ,Clk - Q delay ,setup time and hold time.

#### Note :triggering of DFF and Dlatch (setup and hold time) occur at sampling points. Therefore, for DFF it will be at posedge or negedge of Clk and for Dlatch it will be at negedge or posedge of Clk (pos level Clk or neg level clk). ------- IMPORTANT.


![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/0fce30af-6413-47b5-81cf-18be84fca5e1)

3. Timing path - the path for data to move from a) clk of one flop to the input of next flop (reg 2 reg) b) input to output (not present usually IO path) c) input to flop d) clk of flop to output (c,d are IO Timing Paths). The max Tclk value will be the critical path of the design as it will be the least clk delay that can be used for the design.

#### Note :a) MAX constraint :- Tclk >= Tcq + Tcombi + Tsetup --> Data path(max) > Clk path(min) b) MIN constraint :- Thold <= Tcq + Tcombi --> Data path(min) < Clk path(max)

## Basic STA :

### Constraints

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/69f55fa8-ccc4-4518-bf2f-4bb857bcddca)

The constraints are applied based on the design specifications

1. reg2reg --> contrained by clk -> Tcombi will be squeezed to compensate.

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/96f55216-4818-4c94-86e2-8d47321aacd8)

2. in2reg --> constrained by clk ,input external delay and input transition . Input logic will be squeezed to compensate.
input external delay

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/71cea486-b225-4079-bf83-39812471a91b)

input transition delay --> incresase input logic delay which needs to be further squeezed.

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/20c4751b-da85-47c7-9332-a09049d80dd1)

3. reg2op --> constrained by clk ,output external delay and output load (parasitic capacitance). Output logic will be squeezed to compensate

output external delay

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/d5c3d09e-659b-4ef1-aac3-df3dbf4c93fd)

output load (parasitic capacitance) --> incresase output logic delay which needs to be further squeezed.

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/e45ee2aa-536d-4c4d-8181-9c3ee792595e)

4. reg2op and in2reg are called IO Paths and the delay modelling is called IO delay Modelling. (standard interface specifications like SPI,I2C --> industry protocols)

#### NOTE : 1) rule of thumb --> external delay : internal delay is 70:30. 2) IO paths need to be constrained for MAX delay(setup) and MIN delay(hold).

## LABS :

exploring the library file and learning how the files were characterised --> area ,power , delay , capacitances , input (rise , fall) transistion , pin attributes --> direction,function,Clock pin,Timing sense and type etc , Power pin conncetions ( since logic gates are nothing but CMOS --> VGND , VPBN etc), and other necessary information.

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/25f309d4-87b5-4fd9-9a11-6e255be21c3a)
![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/5fb33836-90c4-4ebc-9628-52b4d5e905d0)

* Lookup tables were also present in the lib file so that tool is able to select the necessary o/p based of the 2 indexes. Eg indexes --> input transition and output capacitance o/p --> timing delay. in case the specified values dont lie in the indexes the range in which the values lie is taken and interpolation is done obtain the value at the specified point.

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/9cd8c785-afcf-49f3-bb42-e9fab4f27a7f)

similarly sequential cells will also have such factors and there exist more dependencies of one pin o/p on the other pin o/p --> related pins. They will also have Clock pins --> There timing type will be specified based of the type of flop it is (rising_edge or falling_edge --> posedge or negedge). The setup/hold time claculation part should also be specified to the tool as "setup_rising" or "setup_falling" to let the tool know at what edge of clock must the setup time be calculated.

LHS - posedge clk , RHS - negedge clk for DFF - defining type of clock

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/b1228948-0f28-4c70-bf31-03e9f76b3f18)

LHS - posedge clk , RHS - negedge clk for DFF - defining setup time calc

![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/2d9e756b-7e40-4eb2-a7d7-73e6d598c172)

dc shell commands --> in our case we will be using OpenSTA since its a free source // verify if these functions match with OpenSTA


         > list_lib
         > foreach_in_collection my_lib_cell [get_lib_cells */*<the cell you need> { 
	    set my_lib_cell_name [get_object_name $my_lib_cell]; 
	     echo$my_lib_cell_name;
	  }
         > foreach_in_collection my_pins [get_lib_pins <cell name>/*]{  --> my_pins is a loop variable
	   set my_pins_name [get_object_name $my_pins];		--> 'get_object_name' 
	   set pin_dir [get_lib_attribute $my_pins_name direction];   --> 'set' is for variable instantiation ; get_lib_pins/attribute <file_name> <pin/attribute_name>
	   echo$my_pins_name	$pin_dir;                      --> to use a variable we use $<var>; to print a variable echo$<var>
	  }

         > source <script filename>.tcl --> for calling a script file
         > list_attributes -app > a  --> for seeing all defined attributes in a library ; it is fed to file called 'a'.

  A script file called my_script.tcl
  
  ![image](https://github.com/Rohitkadam31/VSD-HDP/assets/148602919/f2fe1632-61b6-4f48-9f90-ae168ec4258c)

  ##### NOTE: Important Constraint Commands 1)get_clocks 2)get_ports 3)get_pins 4)get_nets 5)set_input_transition -min -max 6)set_input_delay -min -max 7)set_clock_latency -source           8)set_clock_latency - 9)set_clock_uncertainty - 10)create_clock -name -per -wave 11)get_attribute 12)create_generated_clock -master -source -div 13) regexp a b

  

 














  

  
  

 









 
     


      






     




               

         













                    








                 
                 
                  
                  









    

    









    
