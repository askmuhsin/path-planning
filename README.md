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
The project code has been divided into four sequential parts   
<b>1. Sensor fusion :</b> `main.cpp [line 253-301]`    
Here the data from the cars sensor fusion module is read.   
Two logics are implemented at this point :
 * Detect if there are any cars directly ahead of ego car in 35m. If so turn the `too_close` flag `true`.    
 * Identify all cars ahead and behind the ego car in all lanes within a set distance and classify them by the lane numbers they belong to. Three counters are used for this `l_lane, m_lane, r_lane`, corresponding to left, middle and right lanes respectively.     
<br/>
<b>2. Speed Control</b> `main.cpp [line 303-311]`    
 * The velocity of the car is initially set to zero, and it is incremented in steps of 0.4 as long as <i>the car is below the
 speed limit and there are no cars directly ahead in collision range.</i>   
 * The velocity of the car is decremented by 0.5 if there is a car ahead. There is a further collision avoidance routine which would switch the speed of the ego car to that of the car directly ahead if the space between them are below 5m `main.cpp [line 276]`.          
<br/>  
<b>3. Switch lane</b> `main.cpp [line 314-334]`     
The switch lane checks the flag `too_close`, if there is a car ahead going slow, it will get ready for lane change. This is done using a `switch` statement. If the car is in the lane 0 it can change to lane 2, if the car is in lane 1 it can either change to lane 0 or 2, and finally if the car is in lane 2 it can change to lane 1.    
Before initializing the lane maneuver the car checks if its safe to perform. This is done using the data from the variables `l_lane, m_lane, r_lane`. The lane change has to consider future position of the cars. There are two scenarios to consider, one the car lagging could suddenly brake, or the car leading could suddenly reduce the speed. By taking into consideration the max speed limit (50mph), it became clear that it would be safe to swith lane when there are no cars 15m ahead and behind of the ego car (in the lane to which the ego car is switching). This logic has been implemented on `main.cpp [line 285]`.   
This information is also printed on to the terminal. It shows the number of collision potential cars in a given lane.     
![lane change](https://github.com/askmuhsin/path-planning/blob/master/images/lane_change.gif)     
<br/> 
<b>4. Use spline to generate trajectory</b> `main.cpp [line 303-311]`     

---
# Result
1. The code complies with cmake.   
2. The car is able to drive multiple laps without any incidents, including collisions or breaking speed limit.   
3. At all times the max acceleration and jerk is kept in acceptable range.   
4. The car changes lanes when ever it is feasible and necessary.   

Watch full lap here :    
[![path_planner_image](https://github.com/askmuhsin/path-planning/blob/master/images/thumbnail.png)](https://www.youtube.com/watch?v=E69RmCp4i3Y "Path planner")
