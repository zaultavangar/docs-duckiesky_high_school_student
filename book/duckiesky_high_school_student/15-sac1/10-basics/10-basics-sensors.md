# Intro to Sensors {#sac1-basics-sensors status=ready}

**Explain the definition of roll, pitch, and yaw.**

<figure>
    <figcaption>Roll, Pitch, and Yaw Diagram (https://upload.wikimedia.org/wikipedia/commons/0/04/Flight_dynamics_with_text_ortho.svg)</figcaption>
    <img style='width:12em' src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/Flight_dynamics_with_text_ortho.svg/1200px-Flight_dynamics_with_text_ortho.svg.png"/>
</figure>

With the help of this picture, teacher introduces the terms roll pitch and yaw, and then asks the students to identify which of the sensors measure each of them (IMU for roll and pitch, camera for yaw)

**Answers for Class Discussion Questions**
<!-- gwnote: I think it would be good to restate the questions heres -->
Question 1:

A: Analog-to-Digital Converter (ADC)! [Here (Material 3.15)](https://docs.duckietown.org/daffy/opmanual_sky/out/build_materials_included.html) is how it looks like. 
<!-- gwnote: use this link for a more specific link that takes user to ADC: (https://docs.duckietown.org/daffy/opmanual_sky/out/build_materials_included.html#sub:materials-adc)  -->
<!-- gwnote: a little info on how an ADC works could be useful, or a link for further info -->
<div class='requirements' markdown="1">

Voltage or Current is produced by the sensors -> amplification (convert to voltage if necessary) -> ADC
<!-- gwnote: good place to use the term "transducer. explain why signal needs to be amplified (sensor output might only change a very tiny amount, so we want to make the change bigger by multiplying the output by some value). perhaps giving an example would be good to or exercise in the teacher book -->
</div> 

<figure>
    <figcaption>Analog and Digital Signal Diagram</figcaption>
    <img style='width:12em' src="https://www.allaboutcircuits.com/uploads/articles/An-Introduction-to-Digital-Signal-Processing-(1).png"/>
</figure>

Question 2:

A: Interpolation (estimate the data points in between known data) and extrapolation (using the current trend to predict the future data)

<figure>
    <figcaption>Interpolation and Exterpolation Graph</figcaption>
    <img style='width:12em' src="https://storage.ning.com/topology/rest/1.0/file/get/2656751898?profile=original"/>
</figure>

Question 3:

A: 
<!-- gwnote: would it be worth explaining what it means to cut the frequencies? I think it is also important to explain why averaging removes noise, but also the downfall of averaging: we can't track fast changes. This is a design tradeoff. Ex: We could average the IR measurements for a "smoother" height reading, but it would take longer for the height to update if the drone moves up or down quickly.  -->
    - Filtering Frequencies: cut the frequency measurements that are unreasonably high or low

    - Combining data from multiple sensors

    - Cleverly decide which data are trustworthy

