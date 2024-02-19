# InstrumentConnect-Scripts
Python scripts for InstrumentConnect


import pylablib as pll
import time

# Connect to the APT controller
controller = pll.APTController()

# Connect to the motor
motor = controller.connect_motor(serial_number="your_motor_serial_number")

# Home the motor (optional, if needed)
motor.home()

# Set velocity and acceleration parameters
motor.set_velocity_parameters(velocity=10)  # Set velocity to 10 mm/s
motor.set_acceleration_parameters(acceleration=5)  # Set acceleration to 5 mm/s^2

# Move the motor to a specific position
target_position = 100  # Specify the target position in mm
motor.move_to(target_position)

# Wait for the motor to reach the target position
while not motor.is_in_motion():
    time.sleep(0.1)

while motor.is_in_motion():
    time.sleep(0.1)

# Print the current position
print("Current position:", motor.get_position())

# Disconnect the motor and controller
motor.disconnect()
controller.disconnect()
