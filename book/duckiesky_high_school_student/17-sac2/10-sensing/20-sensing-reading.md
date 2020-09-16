# Reading Sensors {#sac2-sensing-reading status=ready}

## Background

The introduction to Sensors lesson explained the importance of sensors to robots, and the specific sensors used on the drone. The sensor calibration lesson demonstrated how to convert the sensor output into a useful measurement with units. Specifically, the voltage output of the IR sensor was calibrated to obtain distance measurements in meters. This calibration is important because it will allow the drone to know how high above the ground it is, which allows the user to control how high they want the drone to fly. The next step is to create a way for the drone to read these calibrated measurements so that it can use them while flying. This lesson contains the background knowledge for making a sensor and computer "talk" to each other, as well as instructions to write a python script that allows the Pi to read values from the ADC, and convert into calibrated distance measurements.

### Analog to digital conversion
As you've learned, sensors can produce either digital or analog outputs. If the sensor produces an analog output, like the IR sensor, then it is easy for a human to read the sensor value using a multimeter; however, it is not possible for most computers, like the Pi, to read the output since they can only read digital signals. Recall that this problem was solved by introducing the analog-to-digital converter, or ADC. The new problem that arises is how to read the sensor using the Pi.

### Communication protocols
In order for two digital devices to communicate, the device that is sending the information and the device that is receiving the information must speak the same language. For the IR sensor, the device that is sending the information is the ADC, and the device that is receiving the information is the Pi. In this case, the information is the digitized IR sensor measurement. In the world of digital devices, the "languages" are called **communication protocols**. The communication protocol used by the ADC and the Pi is called I2C (pronounced "I squared C" or "I two C"). I2C is a **serial** communinication protocol, which means that information is sent sequentially. For example, if the ADC wanted to send the binary value `1011`, it would need to first send `1`, then `1`, `0`, and finally `1`. There is lots to learn about different communication protocols, their use cases, and how they are implemented. While it can be easy to get lost in the details, it is important to keep the goal in mind: to create a way for digital devices to communicate.

### Software libraries
Fortunately for programmers, the nitty-gritty of communication protocols are handled for us by software libraries that contain **classes** and **methods** that allow other programmers to talk to the devices. The library that will be used for the ADC is called the created by Adafruit to make it easy for programmers to use their device. Here is the [github repository](https://github.com/adafruit/Adafruit_Python_ADS1x1) for this library for reference, but all you need to know is that this is what makes it easy to use the ADC.

## Activity 1: Reading ADC values
Let's begin writing a Python program to read values from the ADC. We will walk through the code line-by-line, and you can either type the code, or copy and paste it.

### Power up your Pi
Plug in the battery, connect to your drone's wifi, and to browse to its code editor: [192.168.42.1:8081](http://192.168.41.1:8081).

### Create a new directory
Create a new folder for your code in the `~/ws/src/pidrone_pkg` directory and name it `student`

### Create a new file
Create a new file in the `~/ws/src/pidrone_pkg/student` directory and name it `ir.py`

### Import the library
Import the Adafruit_ADS1x15 library using the Python import syntax. When you import a library, you have access to all of the functions, classes, and methods that are included.

```
# import the library
import Adafruit_ADS1x15
```

### Create an ADS1115 instance
The Adafruit_ADS1x15 library contains a class for the ADS1115 device, which is the ADC on your drone. You will create an instance of this class using a special method called the **constructor**. Notice that for the ADS1115 class, the constructor takes in no arguments.

```
# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()
```

### Read the ADC value

Once you've created an instance of a class (also called an **object**), you can use the methods that are defined within that class. The method that is used to read a single value from the ADC is called `read_adc`, and it takes in two arguments: the ADC gain and channel number.

**Gain**: If an analog signal is small, then you may want to amplify it, or multiply it by a larger number, in order to make it easier to read. The number that you multiply the signal by is called the gain. According to the [ADC datasheet](https://cdn-shop.adafruit.com/datasheets/ads1115.pdf) on Page 13, Table 3, the gain that should be used between -4.096 and +4.096 Volts is 1. Recall that the IR sensor measures between about 0 and 3 V.

**Channel Number**: The ADC has four input channels labeled "A0" to "A3". If you recall from Build Part 2, the yellow IR sensor wire was soldered into "A0". Therefore, the channel number you will use is 0.

Let's create **global variables** for the gain and channel number at the top of our script so that we  can use these variables everytime we want to read the ADC. Global variables are values that can be referenced by name anywhere in a script. Typically, global variables are written in all capital letters.

```
# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0
```

Now that we've stored the method arguments, let's read from the ADC!

```
# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# read the adc value
adc.read_adc(CHANNEL, GAIN)
```

It doesn't do us much good just to read the value, let's store the value and print it so we can see what it is:

```
# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# read and store the adc value
value = adc.read_adc(CHANNEL, GAIN)

# print the adc value
print(value)
```

### Run the Python Script
Now that we've written the script to read from the ADC, let's test it out!

1. Copy and paste the final code into your ir.py file.

1. Open a new terminal: Menu (top left) > Terminal > New Terminal

1. In the terminal, navigate to the student directory: `cd ~/ws/src/pidrone_pkg/student`

1. Run the script: `python ir.py`

If all went well, a number should print out in the terminal. Congrats on reading the ADC!

If you get an error, try copying and pasting the code again.

To run the script again, simply press the up arrow on your keyboard and press enter. Try running the script while holding the drones at different heights.

Q: Are there any similarities between this value and the value that you read with the multimeter?

A: You'll find out in activity 3!

## Activity 2: Creating a Loop
It's not very fun or useful to have to re-run the `ir.py` script everytime you want to take a measurement. Since our goal is for the drone to know how high it is flying, we don't want to have to run the script each time the height of the drone changes (which is quite often!). Fortunately, there is a programming tool called a **while loop**, which lets us rerun certain lines of code  while some condition holds true. Let's add a while loop to our script so that it keeps printing out the ADC output until we tell it to stop.

### Add the while loop
The simplest condition for a while loop is the boolean, True. If we use True as the condition for the while loop, the loop will never stop, and the script will continuously read and print the ADC output.

```
# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# loop to continuously read and print the ADC output
while True:

  # read and store the adc value
  value = adc.read_adc(CHANNEL, GAIN)

  # print the adc value
  print(value)
```

Notice that the reading and printing lines are indented. Anything that is indented after the while loop is repeated.

### Run the Script
Follow the same steps as before to run the script now that we've updated it. When you want to stop the script, you will need to press the `control` (ctrl) key, and while holding this key down, press `c` on your keyboard.

### Slow down!
As you'll see the values are printing out *really* fast! The while loop is running as fast as the Pi can go; unfortunately, allowing this to happen uses up the Pi's computing resources, and slows down the other processes on the Pi. How about we wait 1 second between measurements to slow down the loop; this will also make it easier for us to read the values being printed.

In order to wait 1 second in between readings, we must import the time library. Let's import this at the top of our file, next to the other import statement. Then, we can use a function in the time module to make the loop wait for one second. This function is called `sleep`, and it takes in one input, which is how many seconds you want the loop to sleep for. We'll use one second.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# loop to continuously read and print the ADC output
while True:

  # read and store the adc value
  value = adc.read_adc(CHANNEL, GAIN)

  # print the adc value
  print(value)

  time.sleep(1)
```

### Run the Script
Copy the changes to your `ir.py` script, and run it on your drone.

## Activity 3: Navigating a Python Library

In the previous activity, you used the Adafruit_Python_ADS1x1 library to read values from the ADC. The instructions walked you through writing the code line by line. To promote self-efficacy, we will take a moment to explain how we figured out how to use this library, and how, in general, you can figure out how to use any library that you want. For example, if you later want to add a different range sensor to your drone instead of the IR sensor, you will need to find a library for the sensor and figure out how to use it.

### Search for your hardware device
The simplest way to find a library for your device is often to read the documentation on the website you bought it from. For the ADC, this was originally purchased from  [Adafruit](https://www.adafruit.com/product/1085), and their webpage include instructions on how to read the sensor, and what library to use.

### Look for examples
Once you've found a library, the next step is to look through the documentation to see if the people who wrote the library also included instructions for how to use it. These instructions are often written in a file names `README`. If there are no instructions, the next option is to look for examples, or the worst case scenario: read through all the code to figure out how it works.

A lot of learning to code involves looking at previous examples and then implementing them for yourself. Most libraries include example scripts that demonstrate the basic functionality of the library. Typically, these example scripts provide enough information to use the library and adapt it to your own needs.

For the ADC, there is no valuable README with instructions, but there are examples. If you click on [this link](https://github.com/adafruit/Adafruit_Python_ADS1x15), it will bring you to the github respository for the library. If you click on the `examples` folder, and then on the `simplest.py` file, you will see a script that demonstrates how to read each channel of the ADC, and then wait for 0.5 seconds before repeating this loop. Looks pretty similar to the script you just wrote, huh?

## Activity 4: Function Composition
Now that we can continuously read the ADC output, we're one step closer to providing useful height measurements for the drone. Remember, our goal is to give the drone information about how high it is above the ground. In the previous lesson, you calibrated the output of the IR sensor to obtain a distance (in meters) from the IR sensor voltage. In this lesson, you wrote a script to read the output of the ADC. The problem that remains is how we can use your previous calibration to convert the ADC output into a height reading. The solution to this problem requires knowledge of the relationship between the ADC output and the IR sensor output, as well as a handy tool called **function composition**.

### Relationship of ADC output to IR sensor Output
Based on how an ADC works, we know that the ADC output is **directly related** to the IR sensor output. A direct relationship means that as one value increases, so does the other. Recall that as the IR sensor moved from 10cm to 50cm from an object, the voltage decreased. Similarly, if you observe the ADC output as the IR sensor is moved from 10cm to 50cm, the value decreases. The ADC value does not have a specific unit; based on how the ADC works, the output is typically referred to as "raw ADC counts". Let's represent the relationship mathematically using the symbols $a$ for the ADC output, $c$ for the constant, and $v$ for the IR sensor output:

\[
    v = c \times a
\]

If we want to show that the voltage is a function of the raw ADC counts, we can write the equation as follows:

\[
    v(a) = c \times a
\]

We can rearrange the equation to solve for $c$:

\[
    c = \frac{v(a)}{a}
\]

### Find the Constant
Use your multimeter and your `ir.py` script to get the value for v(a) and a. Plug these values into the above equation to find the value for $c$. To do this, position the IR sensor between 10-80 cm from an object, then run your ir.py script. Without moving the IR sensor, read the voltage. Divide voltage by the value printed in the ir.py script, and you've got $c$ !


### Function Composition
Your calibration from the previous lesson was a function of the voltage.
If we can find a conversion from raw ADC counts to Volts, then we can use our our same calibration function from before!

Let's write down all of the formulas that we know:

First, your calibration from Volts to distance:
\[
    d(v) = m \frac{1}{v} + b
\]

Second, your conversion from raw ADC counts to Volts:
\[
    v(a) = c a
\]

Since the Pi is able to read the raw ADC counts, but our calibration is a function of Volts, we need to combine the above formulas to create a calibration function from raw ADC counts to distance. Fortunately, we can **compose** the functions to find:

\[
    d(v(a)) = m \frac{1}{v(a)} + b
\]

By substituting the formula for $v(a)$, we are able to create a calibration function from raw ADC counts to distance!

\[
    d(a) = m \frac{1}{c a} + b
\]


### Dimensional Analysis

The function compositions states that the distance is a function of voltage, which is a function of raw ADC counts. Let's plug in the units to our function and use dimensional analysis to verify that the final unit is meters:

\[
    \textrm{meters} = \textrm{meters} \times \textrm{Volts} \frac{1}{\frac{\textrm{Volts}}{\textrm{raw ADC counts}} \times \textrm{raw ADC counts}} \textrm{raw ADC counts} + meters
\]

After canceling the units on the top and bottom, we get meters! At this point, we have all that we need to get a distance measurement on the Pi.

## Activity 5: Calibration in Code
In activity 4, we found that we can convert the raw ADC counts to distance using the function:

\[
    d(a) = m \frac{1}{c a} + b
\]

Let's add this function to our `ir.py` script to do the conversion.

### Define the function
To define a function in Python, you simply use the keyword, *def*, followed by the function name and parentheses that contain the function arguments. Here is the general syntax for defining a function:

```
def my_function(arg1, arg2, ..., argN):
  do something here
  do something else here
  return someValue
```

Now, define the calibration function at the bottom of your ir.py script and call it `get_distance`. It will take in one argument, `raw_ADC_counts`, and it will return the calibrated measurement

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  d = m * 1.0/(c * raw_ADC_counts) + b
  return d

# loop to continuously read and print the ADC output
while True:

  # read and store the adc value
  value = adc.read_adc(CHANNEL, GAIN)

  # print the adc value
  print(value)

  time.sleep(1)
```

### Fill in Constants
Unfortunately, this function will throw an error at this point, because neither $m$, $c$, or $b$ are defined. Define these values before computing $d$ by filling in the constants that you found from Activity 4 ($c$) and the previous lesson ($m$ and $b$). If you did not do activity 4, you can use `0.00012438` for $c$. The variables $m$, $c$, and $b$ are called _local variables_ because they are only defined within the _get_distance_ function.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0  # use your own value for m
  b = 0  # use your own value for b
  c = 0  # use your own value for c
  d = m * 1/(c * raw_ADC_counts) + b
  return d

# loop to continuously read and print the ADC output
while True:

  # read and store the adc value
  value = adc.read_adc(CHANNEL, GAIN)

  # print the adc value
  print(value)

  time.sleep(1)
```

### Call the Function
Great job creating the function, now it's time to use it! Call the function in your while loop and print out the raw ADC value, as well as the calibrated measurement.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0  # use your own value for m
  b = 0  # use your own value for b
  c = 0  # use your own value for c
  d = m * 1.0/(c * raw_ADC_counts) + b
  return d

# loop to continuously read and print the ADC output
while True:

  # read and store the adc value
  value = adc.read_adc(CHANNEL, GAIN)

  # call the calibration function
  distance = get_distance(value)

  # print the calibrated value
  print(distance)

  time.sleep(1)
```

### Run the script
Copy the new code to your `ir.py` script, and run it as you did before. Use a meter stick to check if the height measurements are accurate.

Congrats on getting calibrated measurements on your drone!
