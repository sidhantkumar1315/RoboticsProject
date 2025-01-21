# Robotics Project

This file is an Aseba Event Scripting Language (AESL) script designed to control a robot's behavior. It uses event-driven programming to handle button presses, proximity sensor inputs, and timer events for tasks like movement, obstacle avoidance, and line-following.

## Features

### 1. Button Event Handlers
- **`button.forward`**  
  - Sets the robot's state to `FWD` (forward movement).  
  - Both motors are activated with a target speed defined by the constant `TARGET`.
- **`button.backward`**  
  - Sets the robot's state to `STOPPED`.  
  - Stops both motors by setting their target speed to `0`.

### 2. Proximity Event Handler (`prox`)
The robot reacts to proximity sensor readings for adaptive behavior:
- **Line Following**:  
  - If the robot is in the `FWD` state and detects a black line:
    - Stops one motor to make a turn and follow the line.
- **Obstacle Avoidance**:  
  - If both ground sensors detect a black line and a horizontal sensor detects an obstacle:
    - Switches to the `BACK` state and reverses both motors for a duration defined by `BACK_PERIOD`.
  - If horizontal sensors detect an obstacle while moving:
    - Saves sensor data to the `sensors[]` array for further processing.

### 3. Rotation Based on Sensor Input
If sensor values exceed the threshold (`THRESHOLD`), the robot rotates based on obstacle location:
- **Sensor 1 (left)**: Rotate right.
- **Sensor 3 (right)**: Rotate left.
- **Sensor 2 (center)**: Rotate in place.

### 4. Timer Event Handler (`timer0`)
- **State: BACK**  
  - Stops both motors and resets the timer.
- **State: ROTATE**  
  - Resumes forward movement after the rotation is complete.

## Key Constants

- `TARGET`: Speed for forward movement.
- `BLACK_LINE`: Ground sensor threshold for detecting a black line.
- `BACK_PERIOD`: Duration for reversing when backing away from obstacles.
- `THRESHOLD`: Proximity sensor threshold for detecting obstacles.
- `TURN_PERIOD`: Duration for rotational movements.

## How to Use

1. **Load the Script**  
   Upload the `FinalProject.aesl` file to Aseba Studio or another compatible environment.

2. **Run the Script**  
   Connect your robot (e.g., Thymio) to the programming environment and execute the script.

3. **Test the Robot**  
   - Use the forward and backward buttons to control the robot's movement.
   - Place the robot over black lines to observe line-following behavior.
   - Introduce obstacles to test obstacle avoidance.

4. **Modify Constants**  
   Adjust values like `TARGET`, `THRESHOLD`, or `BACK_PERIOD` to fine-tune behavior.

## Requirements

- **Robot**: Thymio or another robot compatible with AESL.
- **Software**: Aseba Studio or a similar tool to load and execute AESL scripts.

## Notes

- The script follows a state-based design to manage movements and responses.
- Calibrate sensors carefully for accurate obstacle detection and line following.
