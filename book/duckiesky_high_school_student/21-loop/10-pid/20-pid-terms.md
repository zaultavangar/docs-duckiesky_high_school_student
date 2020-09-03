# The Three PID Terms {#loop-pid-terms status=ready}

Here is a helpful intro [video](https://www.youtube.com/watch?v=wkfEZmsQqiA) explaining PID controllers
 
### The Three PID Term Definitions

**The Proportional Term**
 
The proportional term produces an output that is proportional to the calculated error:
 
$$ P = K_pe(t)$$

During programming, you would represent this as: 

$$P = K_pe(t_k)$$
 
The magnitude of the proportional response is dependent upon $K_p$ which is the proportional gain constant. A higher proportional gain constant indicates a greater change in the controller’s output in response to the system’s error.
 
The propellers will spin faster the farther away the drone is.
 
**The Derivative Term**
 
The derivative term is determined by the rate of change of the system’s error over time multiplied by the derivative gain constant $K_d$.
 
In terms of calculus, it would be represented like this: 

$$D = K_d \frac{de(t)}{dt}$$

In terms of programming and without the use of calculus, it can be represented by: 

$$D = K_d\frac{e(t_k)-e(t_{k-1})}{\Delta t}$$

The derivative term will do something like: propellors will spin slower the faster the drone is moving. Or a similar example is when drag is pulling harder, the faster the drone is moving. 
 
**The Integral Term**
 
The integral term accounts for the accumulated error of the system over time. The output produced is comprised of the sum of the instantaneous error over time (or simply the instant rate of change in the error) multiplied by the integral gain constant $K_i$.
 
In terms of calculus, the equation would look like this: 

$$I = K_i \int_{0} ^ {t} e (\tau) d \tau$$

With no calculus, the equation would look like this: 

$$I = K_i\sum_{i=0}^k e(t_i)\Delta t$$

The integral term will do something like: propellors will spin faster the longer the drone is away from the desired set point. 
 
### The Overall Control Function
 
The overal control function consists as the sum of proportional, integral, and derivative terms.
 
$$u(t) = K_pe(t) + K_d \frac{de(t)}{dt} + K_i \int_{0} ^ {t} e (\tau) d \tau$$

The figure below summarizes the inclusion of a PID controller within a basic control loop.

<figure>
    <figcaption>PID Controller Block Diagram</figcaption>
    <img style='width:35em' src="https://docs.duckietown.org/DT19/doc-sky/out/assets/data-from-img-pid_controller_block_diagram-a2353f10.png"/>
</figure>
 
### Tuning:
 
Tuning a PID controller is done by setting the conotrl parameters $K_p, K_i, K_d$ to values that fit to be able to get an ideal control response. The three control terms may be correlated and so changing one parameter may impact the influence of another. The general effects of each term are therefore useful as reference, but the actual effects will vary depending on the specific control system.
 
**Effects of $K_p$**:


Increasing $K_p$ will proportionally increase the control output. This causes the system to react more quickly (thereby decreasing the rise time and the settling time by a small amount). Even so, setting the proportional gain too high could cause massive overshoot, which in turn could destabilize the system. Increasing $K_p$ also has the effect of decreasing the steady-state error. However, as the value of the process variable approaches the setpoint and the error decreases, the proportional term will also decrease. As a result, with a P-controller (a controller with only the proportional term), the process variable will asymptotically approach the setpoint, but will never quite reach it. Thus, a P-controller cannot be used to completely eliminate steady-state error.
 
**Effects of $K_i$**:
 
The integral term takes into account past error, as well as the duration of the error. If error persists for a long time, the integral term will continue to accumulate and will eventually drive the error down. This has the effect of reducing and eliminating steady-state error. However, the build-up of error can cause the value of the process variable to overshoot, which can increase the settling time of the system, though it decreases the rise time.
 
**Effects of $K_d$**:
 
By calculating the instantaneous rate of change of the system’s error and using this slope for linear extrapolation, the derivative term anticipates future error. While the proportional and integral terms both act to move the process variable to the setpoint, the derivative term seeks to dampen their efforts and decrease the amount the system overshoots in response to a large change in error (which would greatly affect the magnitude of the proportional and integral contributions to the overall control output). If set at an appropriate level, the derivative term reduces oscillations, which decreases the settling time and improves the stability of the system. The derivative term has negligible effects on steady-state error and only decreases the rise time by a minor amount.


<figure>
    <figcaption>General Effects of Control Terms</figcaption>
    <img style='width:35em' src="https://docs.duckietown.org/DT19/doc-sky/out/assets/data-from-img-control_term_effects_table-e300370c.png"/>
</figure>
