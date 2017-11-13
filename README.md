# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

This project is to use the Proportional-Integral-Derivative controller to fine tune the car so that it will autonomously drive on the given track in simultor.

## PID tuning
I start with PID [0.5 0 0.5] and sooner realized that car veers off the road before the first turn. Then decrease the Kp to 0.2 range and car is able to stay most of track. However car is oscillating a lot. In order to avoid the oscillation, increate the Kd to 1.6 range. The car can stays on the road most of time. Meanwhile, increase the Ki by small number so that car drives to bit close to the center of road.

After handful of iteration, the final parameters is setllted at: [0.17 0.0016 2.1]

The portion of video is here:

[![pid_drive video]](./output/pid_drive.mov)


## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

