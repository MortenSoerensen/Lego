# Group 9

## Lab Notebook 2

**Date:** 21/02 2015

**Group members participating:** Sille, Morten, Alexander, Simon

**Activity duration:** 7 hours

## Goal
We will investigate the NXT ultrasonic sensor and use it to build and program a wall follower similar to the wall follower presented by Fred Martin.


## Plan
Our plan is to solve the 6 exercises in lesson 2 to learn about the ultrasonic sensor and gain some understanding, before we program the wall follower.

## Results
We mounted the ultrasonic sensor on our LEGO robot without any problems. By using the  SonicSensorTest.java[1] program.
### Exercise 1
We started by placing the car with the ultrasonic sensor  in front of different objects that each had different distances.

Figure 1: The actual distances from the robot's ultrasonic sensor to the object. <img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image00.jpg">

![Figure 1: The actual distances from the robot's ultrasonic sensor to the object.](./images/image00.jpg)

The measured physical distances from the robot to the objects are shown on the picture above and are in the table below. We found no difference in the physically measured distances, and the distances measured by the ultrasonic sensor on the robot. All the objects in the table were, as shown, in an upright 90 degree angle, and therefore there will be no disturbing factors influencing the measurements.

| Values                                         | Binder | Robot box | Plastic box  |
|------------------------------------------------|:------:|----------:|--------------|
| Actual physical  distance                      |  27 cm |      49cm | 111cm        |
| Measured distance  with the ultrasonic  sensor |  27cm  |      49cm | 111cm        |

Table 1: Using the setup seen in figure 1 we are comparing the actual physical distances (measured by a ruler) and the distanced measured by the ultrasonic sensor.

After measuring the different objects with flat surfaces, we decided to try with an object with an incline angle. We have a suspicion that the sensor would have a hard time receiving the reflection that the sonic sound it sends, because the angle will lead the sound waves up, and not back to the receiving microphone on the robot.

The material of the object is cardboard and the angle is around 45 degrees with a small inward curve. By placing the robot more than 40cm from the board, the lcd display would show a distance of 255cm indicating that there is no object in front of it.

Figure 2: The ultrasonic sensor of the robot is in front of the angled surface with a distance of >40 cm. <img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image06.jpg" width="600">
![Figure 2: The ultrasonic sensor of the robot is in front of the angled surface with a distance of >40 cm.](./images/image06.jpg)
### Exercise 2
Next we tried putting on the original test program, alfa_03, where there is a 300 msec sample interval between readings and distance. We changed the sample interval of the [SonicSensorTest.java](http://legolab.cs.au.dk/DigitalControl.dir/NXT/Lesson2.dir/Lesson2programs/SonicSensorTest.java) program in the Thread.Sleep() method. We used intervals of 300, 200, 100, 50 and 10.
We then used the same objects and placed the robot at the same distance as in exercise 1 to see if the interval has any effect on the sonic sensors measurement. We quickly conclude after the measurements, that the different intervals had no effect to the sensors values.
Since there is no difference in the behaviour of the robot and sensor, we believe that the thread.sleep() method can be removed without it having an effect on the program, and the time can then be used for other more important programs.

### Exercise 3

<img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image01.jpg" align="right" width="200">
![Figure 3: Here we are measuring how far the ultrasonic sensor can be placed away from the office binder and still measure the distance to it.](./images/image01.jpg)
The maximum distance able to be measured by the ultrasonic sensor is 254 cm, when the sensor don’t find an object the value returned is 255.
In this exercise we try to measure the maximum distance the ultrasonic sensor.
We tried two objects an office binder 28x31cm and a box 60x110cm.

With the office binder we were only able to measure a maximum of 174 cm, if we placed the sensor further away, the program returned 255. We think that this is because of the small surface of the binder, and not enough sound waves hitting the surface.


With the box we were able to register values up to 254 cm.
Sound takes approximately 3ms to travel 1 meter. This means that we cannot do a measurement 2,5 meter away from an object more than once every 10 ms (assuming that it only takes 1 ms to calculate the distance after receiving feedback).

[Comment]: <> (Figure 3: Here we are measuring how far the ultrasonic sensor can be placed away from the office binder and still measure the distance to it.)

### Exercise 4
The TrackerTester program is waiting for an object to come inside a measurable distance (0-254cm).
The error is calculated to be distance - desiredDistance (35cm as default).
If the error is positive, that means that the robot too far away from the object and the power is calculated to be power=pgain*error+minPower.
Is the error is negative the robot will drive backwards using power=pgain*Abs(error)+minPower.
Both engines is using the calculated power value so the robot is only driving straight forward or backwards.

| Setpoint (SP)   | Process variable (PV) | Manipulated variable (MV) |
|-----------------|:---------------------:|--------------------------:|
| desiredDistance |        distance       |                     power |
Table 2: The setpoint is our goal and is called desiredDistance in the program. The process variable is our current sensed position called distance in the program. The manipulated variable is the input to the process. in our case it is the electric current to the motor which corresponds to the power percentage we want to motor to run at, called power in our program.
### Exercise 5
We used the PCparamTracker.java program to change the two variables; Pgain, and MinPower, to observe how the two affect the oscillation of the robots movement when set in front of an object. Without changing any of the values, we observe that the robot drives forward until reaching a distance of 35cm to the object, where it then stops moving.

At first we change the pgain value from 2.0 to 10, and keep the minpower at 50. Then we run the program and observe what happens, while also using datalogger to create a diagram as shown below.

<img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image02.png" style="width:100;height:70">
![](./images/image02.png)

With the first observation we see how the robot kept driving back and forth from the object, but always slowly getting closer to the object. As we can see on the diagram, the oscillation is rapid and constant, but slowly decreasing. The robot never kept still during this run, always driving back and forth.

In the second run we change the pgain value to 20, and keep the minpower on 50.

<img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image03.png" style="width:100;height:70">
![](./images/image03.png)

Here we see how again the robot oscillates between distances. We observe that it keeps going, and doesn’t stop. On the diagram above we see the distance oscillating between 45 and 25, always passing over or under the 35 cm threshhold.

In the third run, we look at the minpower, and change this to 70, while also setting a fairly high pgain of 10.

<img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image05.png" style="width:100;height:70">
![](./images/image05.png)

On the diagram of the third run we see a short oscillation and then an increase before the end. This is because the robot would slowly turn to the right, because of the force of the speed it has when making an abrupt stop, causing the wheels to turn a little, ending with the robot no longer facing the object. What we see though in regards to the oscillation is that the same oscillation occurs as with the previous runs, although there is a difference in number of oscillations pr time. Here we see how the curve takes just under a second, whereas the other runs with 50 minpower, have curves that ake just above a second. This indicates how the robot drives faster with a higher minpower.

In the final run we set the variables to; pgain 2 and minpower 70.
 
<img src="http://krygersorensen.dk/wp-content/uploads/2016/02/image04.png" style="width:100;height:70">
![](./images/image04.png)

We observe the robot again oscillating back and forth, but with small movements. On the diagram we see many small curves, showing how the robot slowly is trying to find the 35 cm threshhold.

### Exercise 6
In this exercise we look at Philippe Hurbain’s wall follower program that he has created by using NQC. We take a look at his program and try to convert it into a java program. See [Wallfollower](https://gitlab.au.dk/mks1234/LegoGroup9/blob/master/WallFollower.java)

We find some important methods in this program that control the movement of the robot in different situations. What Hurbain has done, is he has declared 6 distance thresholds, 3 for turning right, and 3 for turning left. The 3 turn methods are based on whether the robot must turn in place, normal turn, or shallow turn. Whenever the distance sensor measures these thresholds the corresponding turning method is done.

By using the above code, we found some problems. If the robot is too close to the wall when following it, it will not turn hard right when hitting a corner, because the angle of the sensor of 45 degrees, doesn’t registrate the upcoming corner.
Also when coming across an edge, the robot sometimes would have a hard time finding back to the continuing wall. We tried to fix these problems by changing the thresholds and how hard the turns should be, but it would only work if the robot is placed at a certain distance from the wall at start.

After this, we looked at the suggestions on page 179, 5.1.3 exercises in the Fred G. Martin, Robotic Explorations book. The exercise asks for a way to create a progressive turning algorithm for the wallfollower for this we could see how the PIN control method was used to control the turning speed, depending on the distance measured.

We experimented with two programs, the one written based on the NQC-code from Hurbain and another using PID lend from another group.
Although with either program, we still have issues with the robots placement at start, and the corners and edges of the walls. We noticed that our robot has a tendency to turn right, and we are unsure if this is because of low battery, or the wheels might be crooked.


## Conclusion
We find that different materials and angles have an effect on the ultra sonic sensors readings. The max distance the ultra sonic sensor can measure is 255cm.
By turning up the pgain, we find the robot oscilliating alot back and forth, and the same goes for too much power. There is a perfect spot that must be found, that involves the pgain to be a low value.
The PIN method can be used to have the robot act dependently on a sensor value with a simple algorithm.

We wish to improve on the robots behaviour when following a wall. We want to test the program again while the robot has full battery life, to see if it still turns a little to the right all the time. Furthermore it could be interesting writting our own PID-based control algorithm.

## References
[1] Chapter 5, pp. 174-190 of Fred G. Martin, Robotic Explorations: A Hands-on Introduction to Engineering, Prentice Hall, 2001.

[2] [Pid Controller](https://en.wikipedia.org/wiki/PID_controller), Wikipedia

[3] Philippe Hurbain [WallFollower](http://www.philohome.com/wallfollower/wallfollower.htm)

[4] [Ultrasonic sensor](http://www.tik.ee.ethz.ch/mindstorms/sa_nxt/index.php?page=tests_us), Claudia [E-mail](fclaudia@ee.ethz.ch) & Thomas [E-mail](tother@ee.ethz.ch)

[5] [Speed of sound](https://en.wikipedia.org/wiki/Speed_of_sound), Wikipedia