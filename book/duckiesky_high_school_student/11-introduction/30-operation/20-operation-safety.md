# Safety {#introduction-operation-safety status=ready}

 
Teachers should emphasize that the drone students are building is relatively powerful, and can cause harm to them or others if not used safely.
 
#### Case Study: The Midair Collision in 2009
 
There was a collision between a private airplane and a sightseeing helicopter over Manhattan. The result was 9 deaths.
 
There were several causes that contributed to this:
 
 
1) The limitations of the see and avoid concept:
 
9 seconds before collision, the helicopter was not seen from the airplane.
5 seconds before collision, the helicopter was still very far from view.
1 second before collision, the helicopter was too close to be able to act sufficient.
 
By the time the pilot of the airplane saw the helicopter, there was no time/not sufficient enough time to avoid the helicopter.
 
2) Teterboro Airport local controller’s non pertinent telephone conversation (New York Times).
 
The controller was distracted as he was having a phone call. He did not communicate with the pilot and was unable to warn the pilot of a potential crash.
 
3) Inadequate FAA procedures and regulations:
 
There are inadequate FAA proceuures for transfer of communications between ATC facilities along that area of where the crash occured (New York Times).
 
As well, the FAA regulations that not allow for sufficient vertical separation between aircraft flying in the region (Prof Tellex slides).
 
<!-- https://www.nytimes.com/2009/08/15/nyregion/15crash.html
 
https://www.nytimes.com/2009/08/10/nyregion/10collide.html
-->
 
 
#### FAA rules
 
The Federal Aviation Administration (FAA) is a US governmental boday that is responsible for regulating aviation and unmanned aircraft. It regulates flights outdoors, airports, air traffic management, certification of people and aircraft, and protection of US assets. FAA rules do not apply to operations that take place indoors. 
 
Students are considered to be recreational users.
 
Faculty and staff are considered to be non-recreational users.
 
Here are some of the important safety guidelines by the FAA:
 
1. Fly at or below 400 feet 

2. Be aware of airspace requirements and restrictions 

3. Stay away from surrounding obstacles 

4. Keep your UAS within sight 

5. Never fly near other aircraft, especially near airports 

6. Never fly over groups of people 

7. Never fly over stadiums or sports events 

8. Never fly near emergency response efforts such as fires 

9. Never fly under the influence of drugs or alcohol
 
#### Where to fly:
 
You may fly your drone indoors if you have enough space, as FAA rules do not apply to operations that take place indoors.
 
Before flying outside, please check the FAA's website (the Chart  User's Guide or the aeronautical charts provided) to check which airspace you are located in.
 
You may also use the B4UFLY app, which is created by the FAA to help recreational flyers to figure out where they can safely fly and/or any restrictions in a location.
 
#### Possible Sources for Danger:
 
There are several possible sources of danger that can result from the drone:
 
1) applying force to your body
2) energy discharge from the body
3) parts or propellers dislodging from the drone
4) electric shorts and fires
 
#### Safe Environment
 
The Bystander Effect:
 
The more people that are present, the less likely someone will help a victim during a situation.
 
Be wary of this, make sure that if there is a dangerous situation, be cautious and aware, and take action to help those who need it.
 
Make sure that you have a safe environment to fly indoors.
 
Make sure you have equipment:
1) Safety glasses
2) Gloves
3) Walls
4) Distance
5) Net (not required)
 
#### Pre-flight Safety Checklist
 
Before you fly, you should make sure:
 
1. Do I have my safety goggles on?

2. Do I have a safe space to fly? Is there the possibility of the drone flying away or collisions?

    Make sure the surface you are flying over is not reflective, and is not uniform in details. Preferably a highly textured planar surface (ie: poster board with a bunch of scribbles and shapes)

    If outdoors: make sure that you are flying in a safe space that adheres to FAA rules, double check restriction and regulations of your space. Watch out for trees, flying duckies, people, etc. 

    If indoors: make sure that you have an adequate clear area where you can fly a drone around and no obstacles that the drone/you will crash into. 

3. Make sure the propellers, motors, and flight controller are correctly placed and not loose. 

    With the battery disconnected: make sure that the numbers of the propellers and the motors correspond. Also, the arrows on the propellers should be visible from the top of the drone, and the arrows should be going in the same direction as the arrows on the motors.

    The propellers should not be able to spin freely around the motor shaft. Make sure the propellers are tightened down so that they cannot spin freely and there is no gap between the propeller, the motor, and the motor nut.

    Make sure that the flight controller is not loose to ensure that it won’t wiggle around or fall out of position during flight.

4. Make sure there are no dangling wires or wires that are in the way of the propellers. 

    With the battery disconnected, spin the props with your finger and make sure there are no wires in the way.

5. Make sure that the flight controller USB is connected to the Pi. 

6. Inspect the battery for any problems. Check battery level when plugged in.
    
    Make sure that the battery is not swelling, puffing, or smoking (when and when not plugged in or charging). 

    When the drone is connected, you can check the battery level on the web interface. The battery level should generally be above 10V, if it is lower make sure it is charged.  

7. With drone connected, make sure that you are connected to the correct drone.

    You can check this by running the blinkpowerled.sh script in pidrone_pkg

8. With drone connected, make sure there are no node errors. 
    
    Go through each of the screens using ` n, where n is a number 0-5, and make sure there are no errors printed out. It is normal that there may be an error at the top of the screen that says something about not connecting to ROS master, but that is OK because it takes a bit for ROS to startup. Make sure there is other text underneath this error, and that text does not also include an error message.

9. With drone connected, make sure that the IR sensor is working. 
    
    While looking at the web interface, move the drone up and down and make sure you see changes in the IR graph on the web interface

10. With drone connected, check the kill switch and ensure that it works. 

    Press the space bar to arm the drone, and you will see the motors start turning. 
    Press the space bar again to kill/disarm the drone, and you will see the motors stop. 


 
#### First Flight:
 
The first time you fly the drone or start the drone, there may be some situations you may experience/be aware of:
 
- Drone flips: incorrect propellor orientations

- Collisions: no side/back sensors

- Battery mishaps: replace batteries or charge them

- Excessive heat production of the drone: shorts in soldering

- IR Sensor not working: check soldering and voltages

- Motors not responding: check calibration and soldering, run calibration script in terminal

- Haywire flight: check if flight controller is steady, make sure to run calibration script in terminal


 
**Useful Resources and References**
 
[The OSHA Technical Manual on Industrial Robots and Robot System Safety](https://www.osha.gov/dts/osta/otm/otm_iv/otm_iv_4.html)
 

