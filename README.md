from spike import PrimeHub, ColorSensor, Motor

# Initialize Spike Prime components
hub = PrimeHub()
color_sensor = ColorSensor('E')
motor_left = Motor('A')
motor_right = Motor('B')

# Constants for color thresholds
LINE_COLOR = 5  # Change this value according to your line color
TOLERANCE = 3   # Adjust this value to set the tolerance for line detection

# Set motor speeds
BASE_SPEED = 40
MOTOR_SPEED_LEFT = BASE_SPEED
MOTOR_SPEED_RIGHT = BASE_SPEED

# Main loop
while True:
    # Read color sensor value
    color = color_sensor.get_color()

    # Check if the color is within the tolerance of the line color
    if abs(color - LINE_COLOR) <= TOLERANCE:
        # Line detected, move forward
        motor_left.start(MOTOR_SPEED_LEFT)
        motor_right.start(MOTOR_SPEED_RIGHT)
    else:
        # No line detected, adjust direction
        if color < LINE_COLOR:
            # Turn left
            motor_left.start(-MOTOR_SPEED_LEFT)
            motor_right.start(MOTOR_SPEED_RIGHT)
        else:
            # Turn right
            motor_left.start(MOTOR_SPEED_LEFT)
            motor_right.start(-MOTOR_SPEED_RIGHT)
