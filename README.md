# Run Away Robot with Unscented Kalman Filter Bonus Challenge Starter Code

In this project, not only do you implement an UKF, but also use it to catch an escaped car driving in a circular path. The run away car will be being sensed by a stationary sensor, that is able to measure both noisy lidar and radar data. The capture vehicle will need to use these measurements to close in on the run away car. To capture the run away car the capture vehicle needs to come within .1 unit distance of its position. However the capture car and the run away car have the same max velocity, so if the capture vehicle wants to catch the car, it will need to predict where the car will be ahead of time.

<!--more-->

[//]: # (Image References)

[image1]: /build/result.jpg "Sample final score"

#### How to run the program

```sh
1. mkdir build
2. cd build
3. cmake ..
4. make
5. ./UnscentedKF
6. and run the simulator and select Bonus Challenge: Catch the Run Away Car
```

The summary of the files and folders int repo is provided in the table below:

| File/Folder               | Definition                                                                                  |
| :------------------------ | :------------------------------------------------------------------------------------------ |
| src/json.hpp              | Various definitions.                                                                        |
| src/ukf.cpp               | Initializes the filter, calls the predict and update function, defines the predict and      |
| src/ukf.h                 | update functions.                                                                           |
| Src/measurement_package.h | Definition of the package of measures.                                                      |
| src/tools.cpp             | Contains the function that calculate root mean squared error (RMSE).                        |
| src/tools.h               |                                                                                             |
| src/main.cpp              | Has several functions within main(), communicates with the Term 2 Simulator receiving data  |
|                           | measurements, calls a function to run the Kalman filter, calls a function to calculate RMSE |
|                           | these all handle the uWebsocketIO communication between the simulator and it'sself.         |
|                           |                                                                                             |
| src                       | Folder where are all the source files of the project.                                       |
| build                     | Folder where the project executable has been compiled.                                      |
|                           |                                                                                             |


---

Note that the programs that need to be written to accomplish the project are src/ukf.cpp, ukf.h, and main.cpp which will use some stragety to catch the car, just going to the cars current esimtated position will not be enough since the capture vehicle is not fast enough. There are a number of different strageties you can use to try to catch the car, but all will likely involve prediciting where the car will be in the future which the UKF can do. Also remember that the run away car is simplying moving a circular path without any noise in its movements.


Here is the main protcol that main.cpp uses for uWebSocketIO in communicating with the simulator.

INPUT: values provided by the simulator to the c++ program

// current noiseless position state of the capture vehicle, called hunter

["hunter_x"]
["hunter_y"]
["hunter_heading"]

// get noisy lidar and radar measurments from the run away car.

["lidar_measurement"]
["radar_measurement"]


OUTPUT: values provided by the c++ program to the simulator

// best particle values used for calculating the error evaluation

["turn"] <= the desired angle of the capture car "hunter" no limit for the anlge
["dist"] <= the desired distance to move the capture car "hunter" can't move faster than run away car

---

Unscented Kalman Filter Produces results as the x-position is shown as 'px', y-position as 'py', velocity in the x-direction is 'vx', while velocity in the y-direction is 'vy'.

![Final score][image1]

---

#### Discussion

Could improve the parametrization and analyze all cases in which it could be divided by 0 to obtain a better result.
