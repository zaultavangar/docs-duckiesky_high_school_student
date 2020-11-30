# Blinking an LED {#computing-pi-led status=ready}

## Step 1: Blinking the LED in the REPL

There are two types of signals that an LED can provide: **High** and **Low** signals. To turn on the LED, we need to provide **High** signal on the pin we choose, while to turn off the LED we will give a **Low** signal.

After we power up the Pi, navigate to the code [editor](http://192.168.41.1:8081), and open up the terminal, we can type in this line and press **Enter**:

```
gpio -g mode 6 out
```
<!-- gwnote: The BCM was explained in the teacher book, but not the student book. It is worth copying and pasting here for students reference. -->
In this line, the -g option is the option to define the **GPIO BCM** pin as explained earlier. We can use [this page](https://pi4j.com/1.2/pins/model-b-rev2.html) to figure out the numbering. In this case, our LED is connected to **Pin 6** on the Pi, so we designate the corresponding **GPIO6** to run the **Output** mode, which means that it can provide **High** or **low** signal.

Next, we write the signal on GPIO6 to be High by running this command:

```
gpio -g write 6 1
```

At this point, you should see the LED turned on. Similarly, the following command will turn it off by writing the Low signal:

```
gpio -g write 6 0
```

Lastly, we can use the gpio blink command to blink the LED:

```
gpio -g blink 6
```

In the above command, we command pin 6 for a blink, turn on 1 second, turn off 1 second, and so on. Press **CTRL+C** to stop the command.

## Step 2: Blinking the LED using a bash script

An alternative way to blink the LED is to use the gpio commands in bash. Before using them, we need to know the path to the gpio command by using the **which** command in the terminal:

```
which gpio
```

You should get an output of **/usr/bin/gpio** path.
<!-- gwnote: maybe include a brief explanation what the path is -->
Now we are ready to make the bash script. The first step is to create a file such as **blink.sh** with the **touch** command.

```
touch blink.sh
```

Then, navigate to the blink.sh file through the navigator on the left side of the screen editor, open it, and fill in the following script:

```
while :
do
        /usr/bin/gpio -g toggle 6
        sleep 1
done
```

Before we proceed, let's take a closer look to the lines we just wrote. The first line **while：** created an infinite loop that runs the following two lines over and over again. The **toggle** option is an option to write the opposite condition: if the pin is Low, it will be written High, and vice versa. The **sleep 1** means to delay the program for 1 second before it continues.

See: Can you think of a way to change the frequency of blinking by modifying one number in the above script?

After writing our script, we can press **CTRL+X** followed by confirmation by pressing the **Y** button to save it. After that, make the script executable (to give us the permission to run it with the **+x** option) with the **chmod** (change mod) command.

```
chmod +x blink.sh
```

At last, we can run the program with the bash command:h

```
bash blink.sh
```
or
```
./blink.sh
```

The LED should blink. Don't forget to stop it using **Ctrl+C**.

## Additional Reference

[GPIO commands](http://wiringpi.com/the-gpio-utility/)

[Blinking the LED tutorial](https://www.teknotut.com/en/first-raspberry-pi-project-blink-led/)
