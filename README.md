# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

This project is to use the Proportional-Integral-Derivative controller to fine tune the car so that it will autonomously drive on the given track in simultor.


## PID component Description
PID controller has the member method to update the Error for each PID component:
void PID::UpdateError(double cte) {
  d_error = cte - p_error;
  p_error = cte;
  i_error = i_error + cte;

}

where the input cte is from the simulator calcuate the cross track error, i.e. offset from center of lane.
The differential error d_error equals to current cte - p_error, this is the delta between current CTE and previous timestamp CTE.
The proportional error p_error equals to the input cte, i.e. p_error = cte;
The integral error equals to all cte error cumulated so far, i.e. i_error = i_error + cte;

the overall error is calculated in following formula in TotalError method:
    -(Kp * p_error + Ki * i_error + Kd * d_error)

if the PID just has the P component, the data shows that the car will have error, i.e. overshoot and then oscilate along center of lane. one the error keeps becoming bigger, the car veers off track and loses control completely. Following short video shows the [Kp, Ki, Kd] = [0.17 0.0 0.0]. the car can not even reach first turn of road.

[kp_only](./output/Kp_only.mov)

Now, in order to avoid the overshoot and marginal stability of P component only, the derivative component is added, which is temporal error measurement against last timestamp. The effect of derivative error is to counter the steering so overshoot is reduced. when the derivative becomes smaller, the steering angle is depends on proportional error again so it keeps close to the center lane. Following videos shows the two components are used, Kp and Kd, i.e. [0.17 0.0 1.5]. At least now the car can remains on the track and alsmot finish one lap.

[kp_kd_only](./output/Kp_Kd_only.mov)



## PID tuning
I start with PID [0.5 0 0.5] and sooner realized that car veers off the road before the first turn. Then decrease the Kp to 0.2 range and car is able to stay most of track. However car is oscillating a lot. In order to avoid the oscillation, increate the Kd to 1.6 range. The car can stays on the road most of time. Meanwhile, increase the Ki by small number so that car drives to bit close to the center of road.

After handful of iteration, the final parameters is setllted at: [0.17 0.0016 2.1]

The portion of video is here:

[pid_drive video](./output/pid_drive.mov)


## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

