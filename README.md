# LNS REMOVAL & REPLAN

The removal and replan functions are from [MAPF-LNS](https://github.com/Jiaoyang-Li/MAPF-LNS). This repository is directly modified based on [MAPF-LNS](https://github.com/Jiaoyang-Li/MAPF-LNS) and enables users to call the removal and replan functions multiple times without changing the current state.


## Installation 
The code requires external libraries 
BOOST (https://www.boost.org/) and Eigen (https://eigen.tuxfamily.org/). 
An easy way to install the required libraries on Ubuntu:    
```shell script
sudo apt update
```
- Install the Eigen library (used for linear algebra computing)
 ```shell script
    sudo apt install libeigen3-dev
 ```
- Install the boost library 
 ```shell script
    sudo apt install libboost-all-dev
 ```
    
After you installed both libraries and downloaded the source code, 
go into the directory of the source code and compile it with CMake: 

```
cmake .
make 
```
## Usage

Step 1: Start the removal replan program, if call the removal function only then set `--replan` to `false`
```shell

./lns-removal-replan --map random-32-32-20.map --agentNum 150 --state map-random-32-32-20-scene-1-agent-150.json --pprun 6 --adaptive_weight 1 1 0 --num_subset 20 --uniform_neighbor 0 --neighborSize 8 --replanTime 0.6 --destroyStrategy RandomWalkProb --replan true

```

- map: the .map file downloaded from the MAPF benchmark
- agentNum: number of agents in the current map
- state: path to the current state JSON file, key: agent id, value: list of agent location in 2D x, y coordinate, check `map-random-32-32-20-scene-1-agent-150.json` as an example
- pprun: number of times to run the PP replan algorithm
- adaptive_weight: weight for the adaptive algorithm; adaptive_weight [RANDOMWALK, INTERSECTION, RANDOMAGENTS], default [1,1,1]
- uniform_neighbor: (0) fixed nb_size specified by --neighborSize (1) nb_size sample from {2,4,8,16,32} (2) nb_size sample from 5~16

You can find more details and explanations for all parameters with:

```
./lns-removal-replan --help
```

Step 2 : Input the current state JSON file and weight for Adaptive strategy `--adaptive_weight` (optional) and PP replan time limit `--replanTime` (optional) to get the removal and replan information
```
--state map-random-32-32-20-scene-1-agent-150.json --adaptive_weight 1 1 0 --replanTime 0.6
```

## References
[1] Jiaoyang Li, Zhe Chen, Daniel Harabor, Peter J. Stuckey, Sven Koenig.
Anytime Multi-Agent Path Finding via Large Neighborhood Search.
In Proceedings of the International Joint Conference on Artificial Intelligence (IJCAI), pages 4127-4135, 2021.         

 

 
