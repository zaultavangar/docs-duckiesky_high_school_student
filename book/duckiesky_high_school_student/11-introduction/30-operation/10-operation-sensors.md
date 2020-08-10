# Sensors and Actuators {#introduction-operation-sensors status=ready}

#### Important Vocabulary 

<div class='requirements' markdown="1">
 
**Sensors** - parts on a robot that allow it to _sense_, or estimate, its own conditions or environment
 
**Actuators** - parts on a robot that use energy to _interact_ with its environment
 
**Controller** - connects the input from the sensors to create an output from the actuators in order to accomplish a goal
 
</div>


#### Sensors in your drone:
 
 
1. **Infrared Sensor (IR)** - measures the distance to an object (or the ground) using infrared beams, then uses the cable to report it
 
 
<figure>
   <figcaption>IR + IR Sensor Cable</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-ir-36e36345.png"/>
</figure>
 
 
 
2. **Camera** - observes 2D images of the world to allow the drone to determine its planar position and speed
 
<figure>
   <figcaption>Camera (Pi Cam) + Flexible Flat Cable (FFC)</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-picam-082ec991.png"/>
</figure>

3. **Inertial Measurement Unit (IMU)** - sensor on your flight controller (FC) that allows the drone to tell how it is accelerating and rotating in all 3 dimensions
 
<figure>
   <figcaption>Flight Controller (FC) with IMU</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-fc-7d71a642.png"/>
</figure>


#### Actuators in your drone: 

1. **Motors** - actuators that spin at a variable RPM (revolutions per minute) depending on how much power it recieves (quantity = 4)
 
<figure>
   <figcaption>2 CW and 2 CCW Motors</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-2205_2300kv_brushless_motors_red-5ef15e4a.jpg"/>
</figure>
 
2. **Propellers** - device with blades attached to motors to turn rotational motion into thrust (quantity = 4)
 
<figure>
   <figcaption>2 Clockwise and 2 Counterclockwise Blade Propellers (with Extras) </figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-props-6ff462ed.png"/>
</figure>
 
3. **LED** - actuator that lights up that you will be using in some experiments

TODO: insert picture of what the LED looks like or delete it if it's not in the drone kit

#### Controllers in your drone: 

1. **Electronic Speed Controllers (ESCs)** - small computers that react extremely quickly to accomplish to simply keep the motors spinning at a particular speed by sending it a variable amount of power based on the input it recieves (quantity = 4)
 
<figure>
   <figcaption>1 ESC for each Motor</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-esc-1f0c9494.png"/>
</figure>
 
2. **Flight Controller** - computer that connects the IMU sensor to the ESCs and motors to react quickly in order to fly the drone at a particular angle
<!--this definition is wordy-->
 
<figure>
   <figcaption>Flight Controller</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-fc-7d71a642.png"/>
</figure>
 
3. **Raspberry Pi** - more powerful computer that accomplishes a complicated goal, such as flying at a particular speed or to a particular position (it excecutes specific code loaded via an SD card)
 
<figure>
   <figcaption>Raspberry Pi Model B</figcaption>
   <img style='width:16em' src="https://docs.duckietown.org/daffy/opmanual_sky/out/assets/data-from-img-new-pi-f1992335.png"/>
</figure>