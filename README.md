# CarND-Path-Planning-Project
Project done as part of the Self-Driving Car Engineer Nanodegree Program.    
Read more here : [Udacity](https://www.udacity.com/course/self-driving-car-engineer-nanodegree--nd013).

---
### Simulator.
Project requires the following open source simulator : [link](https://github.com/udacity/self-driving-car-sim/releases/tag/T3_v1.2)

## Basic Build Instructions
1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./path_planning`.

---
## Dependencies

* cmake >= 3.5
  * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `install-mac.sh` or `install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
 
---
# Path Planner Objective
The goal of the path planner is to generate a safely navigatable trajectory along a 3 lange highway with other traffic. The speed limit of the highway is 50MPH (~80km/h), other cars are expected to follow speed limit (+- 10MPH).    
The car is also expected to reach the destination with minimum time while meeting the following standards in the order of priority :   
1. Physical Feasibility (Basically stay nonholonomic & no teleportations!!!)    
2. Safety (Car must at all times try to stay in the middle of a lane, except when lange changing. No collisions, or running over objects)    
3. Legality (Traffic rules including speed limit, one-way rules, should be duely followed at all times)    
4. Comfort (no acceleration over 10 m/s^2 and jerk over 10 m/s^3)   
5. Efficiency (Reach destination in minimal time, while following the above rules)      

---
# Discussion

![lane change](https://j.gifs.com/ZVo6N8.gif)

---
# Result
1. The code complies with cmake.   
2. The car is able to drive multiple laps without any incidents, including collisions or breaking speed limit.   
3. At all times the max acceleration and jerk is kept in acceptable range.   
4. The car changes lanes when ever it is feasible and necessary.   

Wath full lap here :    
[![path_planner_image](https://github.com/askmuhsin/path-planning/blob/master/images/thumbnail.png)](https://www.youtube.com/watch?v=E69RmCp4i3Y "Path planner")
