# ENG3-HotwheelParkingLot
 The follwing files are my first foray into using Robotic Arms.
## Table of Contents
* [Table of Contents](#TableOfContents)
* [Planning](#Planning)
* [Research](#Research)
* [Design](#Design)
* [Building](#Building)
* [Coding and Wiring](#Coding)
* [Problematic_Situations](#ProblematicSituatuions)


LINK: https://github.com/OneCHSEngr/CircuitPython/blob/main/lib/lcd7/__init__.py

---

## Planning

### The Criteria and Plan
[Criteria Google Doc](https://docs.google.com/document/d/1x2zcYFR73pVGV2NC_2CteQb3-w5JeybZIv0qkrRLdq0/edit?usp=sharing)

<img src="https://user-images.githubusercontent.com/71342195/144874118-67c72556-f5b6-4b3c-b789-f33a8a4ccfe7.png">

### Description
 I have worked out the planning for the CAD to go first so I can work the code around the CAD and not the other way around. If there are major flaws in the CAD, I can always go back and fix them by re cutting or printing them. So far I am following the plan accordingly and there havent been any problems.

## Research

### Ideas and Solutions
 So far there have been a couple ideas on how to move the arm (displayed below). I have used some of the little details to make my arm easier to make and easier to put together with the limited supplies I have. One problem with designing the arm is moving the arm up and down, there are many ways you can move it up and down but there are only a couple that will work with the small space that is available. One of my ideas for moving the the arm up and down is using a servo at the top and spinning it so the arm can go up and down like a bucket in a well. The other idea to get this to work is to make a small pulley system for a string/rope to pull the arm.

### Idea picture
<img src="https://user-images.githubusercontent.com/71342195/145044090-80b25208-9344-40e5-be1a-7c2717f03a7a.jpg">

## Design

### Issues While Designing/ Solutions
 I have tried to make the first idea where I move the arm up and down like a bucket but the arm wouldnt be able to have a full range of motion wile keeping the strings out of the way. The other problem I have with this idea is the amount of space it takes up. So I will be trying the other idea where I use a pulley system and seeign if there is any way I can improve it to make it more compact and efficient.
 
 I realized that both of the ideas I have for moving the arm vertiaclly are the same. So instead of restarting the whole arm I will be continuing with the bucket idea so that I dont waste time. So to fix the lack of space/ the amount of space the servo takes up, I will be expanding the servo horn and making it bigger. 

###

## Coding_and_Wiring

### Code For Both Servos and LCD Screen


```python
import board
import time
import pwmio
from lcd.lcd import LCD
from lcd.i2c_pcf8574_interface import I2CPCF8574Interface
from adafruit_motor import servo
from digitalio import DigitalInOut, Direction, Pull


button1 = DigitalInOut(board.D2)
button1.direction = Direction.INPUT
button1.pull = Pull.UP

button2 = DigitalInOut(board.D3)
button2.direction = Direction.INPUT
button2.pull = Pull.UP

button3 = DigitalInOut(board.D4)
button3.direction = Direction.INPUT
button3.pull = Pull.UP

button4 = DigitalInOut(board.D5)
button4.direction = Direction.INPUT
button4.pull = Pull.UP

i2c = board.I2C()
lcd = LCD(I2CPCF8574Interface(i2c, 0x3F), 16, 2, 8)

lcd.print("To Park Your CarHold Button")
time.sleep(2)
lcd.clear()

pwm = pwmio.PWMOut(board.A2, duty_cycle=2 ** 15, frequency=50)
pwm1 = pwmio.PWMOut(board.A3, duty_cycle=2 ** 15, frequency=50)
my_servo = servo.ContinuousServo(pwm)
my_servo1 = servo.ContinuousServo(pwm1)

while True:
    time.sleep(0.1)
    if button1.value:
        lcd.print("Parking Car at: 1A")
        time.sleep(0.5)
        lcd.clear()
        time.sleep(0.05)
    else:
        lcd.clear()

    if button1.value:
        print("1 forward")
        my_servo.throttle = -0.14
        time.sleep(1.0)
        print("1 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)
        print("1 reverse")
        my_servo.throttle = 0.11
        time.sleep(1.0)
        print("1 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)

    if button2.value:
        lcd.print("Parking Car at: 1B")
        time.sleep(0.5)
        lcd.clear()
        time.sleep(1)
    else:
        lcd.clear()
    if button2.value:
        print("2 forward")
        my_servo.throttle = 0.11
        time.sleep(1.0)
        print("2 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)
        print("2 reverse")
        my_servo.throttle = -0.14
        time.sleep(1.0)
        print("2 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)

    if button3.value:
        lcd.print("Parking Car at: 2A")
        time.sleep(0.5)
        lcd.clear()
        time.sleep(1)
    else:
        lcd.clear()
    if button3.value:
        print("3 forward")
        my_servo.throttle = -0.14
        time.sleep(1.0)
        print("3 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)
        print("3 reverse")
        my_servo.throttle = 0.11
        time.sleep(1.0)
        print("3 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)
        print("2/3 forward")
        my_servo1.throttle = 1
        time.sleep(1.0)
        print("2/3 stop")
        my_servo1.throttle = 0.0
        time.sleep(2.0)
        print("2/3 reverse")
        my_servo1.throttle = -1
        time.sleep(1.0)
        print("2/3 stop")
        my_servo1.throttle = 0.0
        time.sleep(2.0)

    if button4.value:
        lcd.print("Parking Car at: 2B")
        time.sleep(0.5)
        lcd.clear()
        time.sleep(1)
    else:
        lcd.clear()
    if button4.value:
        print("4 forward")
        my_servo.throttle = 0.11
        time.sleep(1.0)
        print("4 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)
        print("4 reverse")
        my_servo.throttle = -0.14
        time.sleep(1.0)
        print("4 stop")
        my_servo.throttle = 0.0
        time.sleep(2.0)
        print("2/4 forward")
        my_servo1.throttle = 1
        time.sleep(1.0)
        print("2/4 stop")
        my_servo1.throttle = 0.0
        time.sleep(2.0)
        print("2/4 reverse")
        my_servo1.throttle = -1
        time.sleep(1.0)
        print("2/4 stop")
        my_servo1.throttle = 0.0
        time.sleep(2.0)

```

### Problematic Situations
 There have been some problems with code not being able to run and the LCD not being suported by the updated software of my board. I fixed the LCD by using an updated library for the LCD I got from Mr. Dierolf. [LCD Library](https://github.com/OneCHSEngr/CircuitPython/blob/main/lib/lcd7/__init__.py), once I used this and made sure everything else in my library was version 7.0 compatible the LCD started working.
 
 I had some trouble with some buttons that I found so I had to solder and wire new ones that I color coded to make it easier to look and at a moments notice and know where everything belongs. Another problem that I had with wiring was trying to get servos to work as some of them worked with the code and some of them didnt, so sortign through the ones that did and didnt was a pain.

