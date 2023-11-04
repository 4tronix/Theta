# MakeCode Package for Robotixlab Theta robot

This library provides a Microsoft Makecode package for [4tronix / Robotixlab Theta robot](https://4tronix.co.uk/theta)

## Driving the robot    
The simplest way to drive the robot is by using the `go(...)` or `goms(...)` blocks.
With each of these blocks you specify Forward or Reverse, and a speed from 0 to 100.

Both motors will be driven at the selected speed and direction.

Move forward at speed 60 forever:

```block
theta.go(RXDirection.Forward, 60)
```

Move backward at speed 100 for 2000 ms:

```block
theta.goms(RXDirection.Reverse, 100, 2000)
```

You can also spin/rotate the robot with the `rotate(...)` or `rotatems(...)` blocks

Rotate left at speed 70:

```block
theta.rotate(RXRobotDirection.Left, 70)
```

Rotate right at speed 50 for 400ms:

```block
theta.rotatems(RXRobotDirection.Right, 50, 400)
```   

## Stopping
When the motor speed is set to zero then it stops. However, we can also use the motor itself to create a reverse generated current to brake much quicker.
This helps when aiming for more accurate manoeuvres. Use the `stop(...)` command to stop with braking, or coast to a halt.

Slowly coast to a stop:

```block
theta.stop(RXStopMode.Coast)
```

Stop rapidly with braking:

```block
theta.stop(RXStopMode.Brake)
```

## Driving the motors individually

If you want more fine grain control of individal motors, use the `move(...)` blobk to drive each motor separately, either forward or reverse.
You can specify the direction (Forward or Reverse) and speed between 0 and 100.
If the left motor turns slower than the right motor, the robot will turn to the left

Drive both motors forward at speed 60. Equivalent to theta.go(RXDirection.Forward, 60):

```block
theta.move(RXMotor.Both, RXDirection.Forward, 60)
```

Drive left motor in reverse at speed 30:

```block
theta.move(RXMotor.Left, RXDirection.Reverse, 30)
```

Drive forward in a leftward curve:

```blocks
theta.move(RXMotor.Left, RXDirection.Forward, 40)
theta.move(RXMotor.Right, RXDirection.Forward, 70)
```

## Making the Robot Drive Straight

The small DC motors used in the theta and many other small robots are not guaranteed to go at the same speed as each other.
This can cause the robot to veer off the straight line, either to left or to right, even when both motors are programmed to go
at the same speed.
We can partially correct for this by adding a direction bias to the motor speed settings.
If your robot is veering to the right, then set the bias to the left.
Conversely, if your robot is turning to the left, then set the bias to the right.
It varies with speed and battery condition etc, but an approximation is that a 10% bias will result in about 15cm (6 inches)
change of course over about 2m (6 feet).

If robot leaves straight line to the right by about 10cm over 2m, bias it to the left by 5%:

```block
theta.MotorBias(RXRobotDirection.Left, 5)
```

If robot leaves straight line to left by 25cm, bias it to the right by 15%:

```block
theta.MotorBias(RXRobotDirection.Right, 15)
```

## Read sonar value

If you have mounted the optional sonar sensor for the theta you can
also use the `sonar(..)` function to read the distance to obstacles.

```blocks
let distance_us = theta.sonar(RXPingUnit.MicroSeconds)
let distance_cm = theta.sonar(RXPingUnit.Centimeters)
let distance_in = theta.sonar(RXPingUnit.Inches)
```

## FireLed Functions

The Theta has 14 FireLeds fitted.
By default, the FireLeds are automatically updated after every setting. This makes it easy to understand.
However, it can slow down some effects so there is a block provided to switch the update mode to Manual or Automatic.

Set all FireLeds to Green (hard-coded RGB color or built-in colour selection - look at Javascript to see the difference):

```blocks
theta.setLedColor(0x00FF00)
theta.setLedColor(RXColors.Green)
```

Clear all Fireleds:

```block
theta.ledClear()
```

Set the FireLed at position 0 to 13 to selected colour. eg. set Fireled 3 to Red:

```block
theta.setPixelColor(3, 0xff0000)
```

Set all the FireLeds to Rainbow (uses the colour wheel from Red to Purple):

```block
theta.ledRainbow()
```

Shift FireLeds up one place, blanking the first FireLed:

```block
theta.ledShift()
```

Rotate FireLeds by shifting up one and replace the first with the last:

```block
theta.ledRotate()
```

There are some more advanced blocks that allow you to select colours using separate RGB values
and select the brightness of the FireLeds.
The brightness is set to 40 by default, but can go as high as 255.
You should be careful not to look directly at them when they are bright as they can damage eyes.

Switch FireLeds Update Mode to Manual or Automatic:

```blocks
theta.setUpdateMode(RXMode.Manual)
theta.setUpdateMode(RXMode.Auto)
```

// Select colour from separate Red, Green and Blue values
// Each of the Red, Green and Blue values can range from 0 to 255
// This example produces a pale blue colour

```block
let myColour = theta.convertRGB(50, 100, 200)
```

Set brightness of FireLeds to 100

```block
theta.ledBrightness(100);
```

## Supported targets

* for PXT/microbit

## License

MIT
