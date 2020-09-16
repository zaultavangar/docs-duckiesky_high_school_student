# Subscriber and Open Loop {#sac2-ros-subscriber status=ready}
In this section we will introduce you to the concepts of PWM, Pulse Width Modulation, building an open loop controller, and writing a ROS subscriber. We will use these techniques to control the brightness of your LED based on the ROS Distance Publisher you just wrote.

## PWM

We begin with a discussion of Pulse Width Modulation. PWM, is the technique used to control the brightness of  an LED, the speed of your drones DC motors, or any type of control where you need to produce an analog type output with digital means.
The Raspberry pi GPIO output pins produce a square wave output, the pins gives us either 3.3V (when turned HIGH) or 0V (when turned LOW). If we wanted to dim an LED with an analog output we could just send half as much voltage, but this option does not exist with the digital outputs on the Rasberry Pi GPIO. Instead what we must do is turn the signal on and off very quickly. If adjust the speed at which the ON and OFF signals are sent then the brightness of the led will be changed.
It would be prudent to discuss the terms associated with PWM.

### TON (On Time): Is the time the signal is high.
### TOFF (Off Time): Is the time the signal is low.
### Period: Is the sum total of on time and off time.
### Duty Cycle: It is the percentage of time when the signal was high in the time of the period.
### Frequency: Is the number of cycles per second (measured in Hz)

Let’s consider running the LED at a 50% duty cycle at 1Hz. The LED would stay on for half a second and would be off for half a second. This would appear as a blink to the human eye. But if we increase this frequency to 100Hz (100 cycles per second) at a 50% duty cycle, the blinking becomes imperceptible to the human eye. Instead the LED appears to be glowing at half brightness. 

## Open Loop Controllers

An Open-loop control system, also called a non-feedback system, is a continuous control system in which the output has no influence of the input signal. Put into other words, in an open-loop control system the output is not measured and is not provided as “feedback” for the input. Instead an open loop system uses a single input command or set point.

A disadvantage of this is the open-loop system has no knowledge of the output condition thus it can’t correct any errors if the preset value drifts, even if this results in large deviations from the preset value.
Because of this lack of measurement of output another disadvantage of open-loop systems is that they are poorly equipped to handle disturbances or changes in external conditions that may affect the output.

Another type of controller is the closed loop controller which we will discuss in the PID control lesson.

A good example of an open-loop system is a timed clothes dryer. The timed clothes dryer will continue to apply heat to wet clothing for the duration of its input even if those clothes are already dry. 

In this lesson we will create an open loop controller based on the distance topic you wrote in the previous lesson to control the brightness of your LED.

## Writing a ROS Subscriber:
