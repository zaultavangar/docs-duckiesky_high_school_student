# Creating a ROS Publisher {#sac2-ros-publisher status=ready}

## Flashback to the sensor reading code

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

## Creating a ROS publisher

We are going to build upon the above code to write a ROS publisher that receives the distance from sensor and publishes it.

### Import the ROS python library and the needed message types.

We are going to use the ROS python library to write the publisher, and, as introduced in the lesson, the floating point message type as well.

See also: Add the line `import rospy` to the top of the program.

See also: Add the line `from std_msgs.msg import Float32` to the top of the program.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# import the ROS python library
import rospy

# import the Float32 message type
from std_msgs.msg import Float32

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0
  c = 0
  b = 0
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

### Create a publisher

We follow the syntax to create a ROS publisher.

See also: Type `distance_publisher = rospy.Publisher('distance', Float32, queue_size=1)` right before the global variables at the top. The first argument is the topic name, the second is the message type, the third serves to limit the number of queued messages in case the subscriber is not receiving fast enough. For the purpose of this assignment, we can just set it to 1.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# import the ROS python library
import rospy

# import the Float32 message type
from std_msgs.msg import Float32

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# The ROS publisher that publishes the distance
distance_publisher = rospy.Publisher('distance', Float32, queue_size=1)

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0
  c = 0
  b = 0
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

### Create an infrared sensor node

It is important to tell rospy the name of your ROS node, otherwise it would not be able to communicate with the ROS Master.

See also: Type `rospy.init_node('infrared_node')` in the next line.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# import the ROS python library
import rospy

# import the Float32 message type
from std_msgs.msg import Float32

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# The ROS publisher that publishes the distance
distance_publisher = rospy.Publisher('distance', Float32, queue_size=1)

# Initiate the IR sensor node
rospy.init_node('infrared_node')

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0
  c = 0
  b = 0
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

### Publish the message in the previously created while loop

See also: Type `distance_publisher.publish(Float32(distance))` right after the line `print(distance)` in the while loop.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# import the ROS python library
import rospy

# import the Float32 message type
from std_msgs.msg import Float32

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# The ROS publisher that publishes the distance
distance_publisher = rospy.Publisher('distance', Float32, queue_size=1)

# Initiate the IR sensor node
rospy.init_node('infrared_node')

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0
  c = 0
  b = 0
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

  # publish the calibrated value
  distance_publisher.publish(Float32(distance))

  time.sleep(1)
```

### Change the structure of the while loop to a ROS manner. (This step is just a change of syntax)

See also: Change the top of the loop from `while True:` to `while not rospy.is_shutdown():`

See also: Change the bottom of the loop from `time.sleep(1)` to `rospy.sleep(1)`.

```
# import the time library
import time

# import the library
import Adafruit_ADS1x15

# import the ROS python library
import rospy

# import the Float32 message type
from std_msgs.msg import Float32

# create an instance of the ADS1115 class
adc = Adafruit_ADS1x15.ADS1115()

# The ROS publisher that publishes the distance
distance_publisher = rospy.Publisher('distance', Float32, queue_size=1)

# Initiate the IR sensor node
rospy.init_node('infrared_node')

# global variables
GAIN = 1
CHANNEL = 0

# define the calibration function
def get_distance(raw_ADC_counts):
  m = 0
  c = 0
  b = 0
  d = m * 1.0/(c * raw_ADC_counts) + b
  return d

# loop to continuously read and print the ADC output
while not rospy.is_shutdown():

  # read and store the adc value
  value = adc.read_adc(CHANNEL, GAIN)

  # call the calibration function
  distance = get_distance(value)

  # print the calibrated value
  print(distance)

  # publish the calibrated value
  distance_publisher.publish(Float32(distance))

  rospy.sleep(1)
```
