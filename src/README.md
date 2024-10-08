Robot Code updated on 10/8/24 by Samuel M.

```
myVariable = 0

def when_started1():
    global myVariable
    Fly_wheel.set_stopping(COAST)
    Right.set_velocity(70, RPM)

def ondriver_drivercontrol_0():
    global myVariable
    while True:
        Left.set_velocity(controller_1.axis3.position(), PERCENT)
        Right.set_velocity(controller_1.axis2.position(), PERCENT)
        Left.spin(FORWARD)
        Right.spin(REVERSE)
        wait(5, MSEC)

def onevent_controller_1buttonX_pressed_0():
    global myVariable
    Ball_slider.spin_for(FORWARD, 90, DEGREES)
    Ball_slider.stop()

def onevent_controller_1buttonL1_pressed_0():
    global myVariable
    Fly_wheel.spin(FORWARD)
    while not controller_1.buttonL2.pressing():
        Fly_wheel.spin(FORWARD)
        wait(5, MSEC)
    Fly_wheel.stop()

# create a function for handling the starting and stopping of all autonomous tasks
def vexcode_auton_function():
    # Start the autonomous control tasks
    # wait for the driver control period to end
    while( competition.is_autonomous() and competition.is_enabled() ):
        # wait 10 milliseconds before checking again
        wait( 10, MSEC )
    # Stop the autonomous control tasks

def vexcode_driver_function():
    # Start the driver control tasks
    driver_control_task_0 = Thread( ondriver_drivercontrol_0 )

    # wait for the driver control period to end
    while( competition.is_driver_control() and competition.is_enabled() ):
        # wait 10 milliseconds before checking again
        wait( 10, MSEC )
    # Stop the driver control tasks
    driver_control_task_0.stop()


# register the competition functions
competition = Competition( vexcode_driver_function, vexcode_auton_function )

# system event handlers
controller_1.buttonX.pressed(onevent_controller_1buttonX_pressed_0)
controller_1.buttonL1.pressed(onevent_controller_1buttonL1_pressed_0)
# add 15ms delay to make sure events are registered correctly.
wait(15, MSEC)

when_started1()
```
