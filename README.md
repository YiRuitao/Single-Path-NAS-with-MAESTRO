# Single Path NAS with MAESTRO
Built on a stable version of MAESTRO. (H. Kwon et al., Understanding Reuse, Performance, and Hardware Cost of DNN
Dataflows: A Data-Centric Approach, MICRO 2019). Given cache sizes and hardware accelerator, you can estimate the inference latency & energy consumption of your input CNN. Now the package supports conv2d blocks, inverted-residual blocks, and squeeze-and-excitation blocks. 

# Package Dependences
C++ compiler (g++)

SCONS build system (scons)

Boost libarary (libboost-all-dev)

Python 2.7 or later

Pytorch  

# How to compile the code
> scons --clean
> scons

# How to run the program
> ./run.sh

# How to change the parameters
Change the contents of "run.sh" For parameters other than listed below, please ignore it; active development is going on them so correct functionailty is not guaranteed.

--print_res=true/false : If set true, MAESTRO prints out detailed cost information to the screen

--print_res_csv_file=true/false : If set true, MAESTRO prints out a csv file that contains various statistics

--print_log_file=true/false : If set true, MAESTRO prints out a log file that contains various information of detailed computation patterns to "log.txt"

--DFSL_file='data/DFSL_description/MnasNet-A1_rs.m' : Specify the target dataflow and layer description file

--noc_bw=64 : NoC bandwidth

--noc_hop_latency=1 : NoC latency per hops

--noc_mc_support=true : NoC multicast support (In current dev version it's always on)

--num_pes=256 : Number of PEs

--num_pe_alus=1 : PE ALU vector width

--l1_size=32 : l1 buffer size

--l2_size=512 : l2 buffer size

# How to change the DNN model and dataflow
Create a DFSL file under "data/DFSL_description" and point the file using --DFSL_file parameter in "run.sh"

For syntax of the DFSL file, please refer to other DFSL files in data/DFSL_description.

### NB: you must put the dataflow under the "data/DFSL_description" directory

# How to profile default models:

cd data/pytorch_example

python main.py --model "MnasNet-A1"

Supports "MnasNet-A1", "MobileNet-V2", "MobileNet-V3(large)", "MobileNet-V3(small)", "ProxylessNet(mobile)" and "SinglepathNAS".

# How to profile self-defined models:

Use main.py, specify the block arguments by yourself as well as stem/head architecture.  

# Experiments:

Hardware configuration:

L1 cache: 128

L2 Cache: 5408

Frequency: 2.2G Hz

| Model                | Params        | Multi&Add | Cycles | Estimated Runtime |
|----------------------|---------------|-----------|--------|-------------------|
| MnasNet-A1           | 3887038(3.9M) | 330M      | 25.3M  | 11.5s             |
| MobileNet-V2         | 3504872(3.5M) | 320M      | 24.0M  | 10.9s             |
| MobileNet-V3(large)  | 5476416(5.5M) | 233M      | 19.8M  | 9.0s              |
| MobileNet-V3(small)  | 2534656(2.5M) | 65M       | 6.39M  | 2.9s              |
| ProxylessNet(mobile) | 4080512(4.1M) | 336M      | 26.2M  | 11.9s             |
| SinglepathNAS        | 4414216(4.4M) | 360M      | 29.8M  | 13.5s             |


# Contributors
Ruitao Yi (ruitaoy@andrew.cmu.edu)

Hyoukjun Kwon (hyoukjun@gatech.edu)

Prasanth Chatarasi (cprasanth@gatech.edu)

Felix (Sheng-Chun) Kao (felix@gatech.edu)
