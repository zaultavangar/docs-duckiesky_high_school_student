# Intro to Sensors {#sac1-basics-sensors status=ready}

**Explain the definition of roll, pitch, and yaw.**

<figure>
    <figcaption>Roll, Pitch, and Yaw Diagram</figcaption>
    <img style='width:12em' src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/Flight_dynamics_with_text_ortho.svg/1200px-Flight_dynamics_with_text_ortho.svg.png"/>
</figure>

Certain sensors on the drone measure Pitch, Roll, and Yaw. The IMU measures roll and pitch; The camera measures yaw. 

Now, let's define some terms from the picture above.

Pitch- The rotation of the flying body around a side-to-side axis. It can be thought of as an “up and down”  motion.  
Roll- The motion of the flying body rocking back and forth. It can be thought of as the wings of a plane "tilting up or down" 
Yaw- The rotation of the flying body along a vertical axis. It can be thought of "twisting left and right".

[Ref:](https://calaero.edu/aircraft-axes-pitch-yaw-roll/)


**Answers for Class Discussion Questions**

Question 1:

<details>
<summary>
<a class="btnfire small stroke"><em class="fas fa-chevron-circle-down"></em>&nbsp;&nbsp;Answer</a>    
</summary>

Analog-to-Digital Converter (ADC)! 

</details>

[Here (Material 3.15)](https://docs.duckietown.org/daffy/opmanual_sky/out/build_materials_included.html) is what it looks like.



<div class='requirements' markdown="1">

Voltage or Current is produced by the sensors -> amplification (convert to voltage if necessary) -> ADC

</div> 

<figure>
    <figcaption>Analog and Digital Signal Diagram</figcaption>
    <img style='width:12em' src="https://www.allaboutcircuits.com/uploads/articles/An-Introduction-to-Digital-Signal-Processing-(1).png"/>
</figure>

Question 2:

<details>
<summary>
<a class="btnfire small stroke"><em class="fas fa-chevron-circle-down"></em>&nbsp;&nbsp;Answer</a>    
</summary>

Interpolation (estimate the data points in between known data) and extrapolation (using the current trend to predict the future data)

</details>


<figure>
    <figcaption>Interpolation and Exterpolation Graph</figcaption>
    <img style='width:12em' src="https://storage.ning.com/topology/rest/1.0/file/get/2656751898?profile=original"/>
</figure>

Question 3:

<details>
<summary> Answer </summary>

- Filtering Frequencies: cut the frequency measurements that are unreasonably high or low, Combining data from multiple sensors, Cleverly decide which data are trustworthy

</details>






   
