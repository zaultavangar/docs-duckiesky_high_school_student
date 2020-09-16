# Bash {#computing-pi-bash status=ready}

## What is Bash

- Connect to the Pi following the [Build Part 1 Checkpoint Instructions](https://docs.duckietown.org/daffy/opmanual_sky/opmanual_sky/out/build_part1_checkpoint.html) from the Operations Manual.
- We will be learning about Bash commands and the terminal, as mentioned in the Networking Unit. It is important to learn how to utilize a terminal as it is the introduction to the inner processes of the operating system, and it will allow us to directly make changes to our drone!
    - We will be using Bash in the next Unit on Blinking an LED to directly see a change on our drone.
- Bash is the language that many shells are written in. Actually, our Pi's shell runs with Bash!
- Now, click on the terminal in the web editor for the Pi and prepare to input text.
    - Follow the first 10 seconds of [this video](https://drive.google.com/file/d/1HvtKNhsjG_dQt2edeJ40WdhmyO649ZOd/view?usp=sharing) if a terminal is not already open.


## Learning Bash

Better: Exercise: Students should do the following steps with Bash commands to test out their knowledge of the terminal. They can do this through the online web editor when connected to the Pi:

- One of the features that a terminal can do is navigate and view the file system of a computer. For instance, folders you would typically find on your home Computer like "Desktop" and "Downloads" are directories. We are just now being introduced to this terminal, so we want to see the directories and files that are in the current location of the file system.
    - To do this, we can input (or enter) the Bash command **"ls"** that prints the files and directories in the terminal. Click on the terminal, type "ls", and hit enter.
        - The terminal will output (or print) all of the files and directories in the current location of the terminal. Remember, we are on the Pi's terminal so all of these files and directories are on your Pi.
- Folders can be within folders, so directories can be within directories! Your terminal is probably in a directory right now; we want to know where we are in our file system, so lets print the current directory name.
    -  The **"pwd"** command prints the current directory: enter "pwd" into the terminal. 
-  Now, we know what directory we are in! Let's say we need to create a directory with a text file in it. There is a convention in Computer Science to print/use "Hello World" when being introduced to a Computer Science principle/language. So, let's name the directory "Hello" and the text file "World". The end goal of this mini-exercise is to print out the text file, which will contain the contents "Hello World".
    - The **"mkdir"** command allows you to make directories: enter "mkdir Hello".
-  Check that the directory has been created by listing the current files/directories
    - Enter "ls" and there should be a new name that represents our directory in the list.
-  We now want to enter into the "Hello" directory to make the "World" file.
    - The **"cd"** command allows us to traverse directories: enter "cd Hello".
    - Enter "pwd" to see that we are in the new directory.
    - Enter "ls" to see the contents of the directory (which should be nothing because we just created it).
-  We can create a text file called "World.txt" within the "Hello" directory at this point.
    - One of the functions of the Bash command **"touch"** is to create files: enter "touch World.txt"
    - Enter "ls" to confirm that the "World.txt" file was created.
    - The **"cat"** command prints text files into the terminal output: enter "cat World.txt". There should be no output because we created an empty text file.
- We need to consider how we can input the contents "Hello World" into the World.txt file. To do this normally, we would just open World.txt in a text editor, type in "Hello World", and save the file, but let's say we only have access to this terminal and we don't want to open any external applications.
    - The **"echo"** command will echo any input back to the output of the terminal: enter "echo I Love Drones!" just to check. You should get an output of "I Love Drones!".
    - A carat (**">"**) with a file name following it added to any Bash command will take the terminal output of that command and put it into the file.
    - We can use the carat to take the output of the echo command and place it in the World.txt file: enter "echo Hello World > World.txt".
        1. A cool feature of the carat is that it automatically creates a text file for you if one does not exist. In fact, we didn't even have to use the "touch" command to create the World.txt file before the above "echo" command!
-  Print the contents of the "World.txt" file.
    - Enter "cat World.txt".
    - Congratulations! You have completed this conventional introductory "Hello World" step! 
- Before continuing, use the VSCode navigator on the left side of the text editor to navigate to the Hello directory and open the World.txt file for viewing purposes (if it's not showing up, you might have to hit the "Refresh Explorer" option).
    -We could have used this to input the text into the World.txt file, but you may not always have this handy web editor when dealing with a terminal.
-  Delete the "World.txt" file
    - The **"rm"** command deletes files: enter "rm World.txt".
-  Leave the "Hello" directory
    - Using ".." as the argument for the "cd" command will allow you to leave a directory, enter "cd ..".
    - Enter "pwd" to confirm that you have left the directory.
-  Delete the now empty "Hello" directory.
    - The **"rmdir"** command will allow you to remove an empty directory: enter "rmdir Hello".
    -  Check that the "Hello" directory has been deleted and is not on the list of files/directories by entering "ls".
- Once you are ready to move on from this exercise, you might not want to have all of the terminal output above lingering around. The **"clear"** command removes all previous output: enter "clear". You can use this at any point to remove previous input/output from the terminal.

## Exploring the Pi's Directories and Files

Better: Exercise: Students should explore the files and directories of their drone's Pi using the following commands: "ls", "cd", "pwd", and "cat". When finished, navigate back to the starting directory.

Warning: Don't delete or change any of the files or directories on the Pi already!

Comment: You can use the up and down arrow keys on the keyboard in the terminal to see previously entered commands. You can use this if you want to reenter a command or reuse parts of a command.

## Using Bash

Better: Exercise: Create a folder that is called "Actuators", create three text files (name them "1.txt", "2.txt", and "3.txt"), and insert the name of a different Actuator on our drone in each of the three files.

<div class='check' markdown="1">

Make sure to delete the "Actuators" directory.

- This time, try to delete the directory without deleting the contents of the directory first.
    - You should get the following error: "rmdir: Actuators/: Directory not empty".
    - Instead, use the command "rm -r Actuators"
        - The "-r" is telling the rm command to delete recursively, which means it will delete all of the files and directories within before deleting the Actuators directory. This is outside the scope of this class, but if you are interested, you can read more about recursive functions [here](https://www.computerhope.com/jargon/r/recursive.htm).

</div>

- Once you are finished, the **"exit"** command will stop the terminal: enter "exit". 