# Networking {#computing-pi-networking status=ready}

## 7 Layers of Abstraction

-  If not for networking, we would not be able to connect to and run our drones, so it's important for us to learn the concepts of Networking!
    - [Learn about](https://edge.edx.org/courses/course-v1:BrownX+CS195R+2018_T1/courseware/0e3596880ec446d8ab63df427e02e9c4/56017f6d3048461b90466ad229ac8df6/?activate_block_id=block-v1%3ABrownX%2BCS195R%2B2018_T1%2Btype%40sequential%2Bblock%4056017f6d3048461b90466ad229ac8df6) the 7 layers of abstraction at our edX lesson.
        1. What is outlined here is the basis of what is used for our computers, mobile devices, and even with our drones.

<!--  
    - Use HTTP and inspect the element
        - Netcat wont work through the drone in the lesson that was made

TODO: Input details based 7 layers of abstraction.
-->

## Control

-  How can we control our computers?   
    - A shell is a programming language that takes input and gives the input to the computer and operating system to analyze and perform the task that the input asks for. 
    - A terminal is a program that allows the user to interact with the shell.
        1. We will learn more about the terminal in the next lesson on Bash, which is the programming language that many terminals run in.
    - SSH (Secure Shell) is a method that allows a user to remotely log in from one computer/device to another. We utilized SSH to connect to our Pi in the past before we implemented the really handy text editor! 
        1. If you would like, you could attempt to follow our [old build instructions](https://docs.duckietown.org/DT19/opmanual_sky/out/build_phase5.html) to connect to the drone over SSH, but this may be a very self guided process (additionally it may not be compatible over Chromebook).

## Networking with our Drone

- Connect the Pi following the [Build Part 1 Checkpoint Instructions](https://docs.duckietown.org/daffy/opmanual_sky/opmanual_sky/out/build_part1_checkpoint.html) from the Operations Manual
    - The text editor on this screen is Visual Studio Code (VSCode). This is a source editor that allows you to edit various files (like text and Markdown files). Use the editor to open and look at the files in the directory.
    - On the bottom of the screen is a terminal that runs in Bash. We will be learning about and directly utilizing this terminal in the next Unit.

