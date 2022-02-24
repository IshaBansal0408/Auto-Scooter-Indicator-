# Auto-Scooter-Indicator

The goal of the project is to create an auto indicator off system that automatically indicates the indicator lights based on the inclination of the vehicle, ensuring that people behind the vehicle understand that the vehicle is turning so that the rider can freely ride the way he wants to.

## The Dataset

The dataset given is ‘ScooterIMUData.csv’ file which contains a total of 334467 data values and 5 columns. The dataset contains the following attributes/columns:
1.	ts: Time at which the reading was taken.
2.	received_ts: Time at which the reading.
3.	device_uuid:  Universally unique identifier for the device.
4.	data_item_name: Gyro meter reading for X, Y and Z axis (labels).
5.	value: Value displayed by Gyro meter for a particular axis in degrees.

## Some Assumptions Made

1.	The scooter is stationary – No Accelerometer reading available
2.	The moment of scooter happens along x (tilting) and y (sideways) axis only and not the z axis (up and down movement).
3.	Initial frame of reference is taken as an ideal position where the scooter has both roll and pitch angle as 0 degrees.
4.	The Gyroscope is placed in such a way that the top is facing the right-hand side of the scooter and the nose of the Gyro is closer to the rear wheel.

## Mathematical Formulas

The mathematical formulas to compute the values of Roll and Pitch angle are shown below. For Equ1. the difference is taken instead of addition because roll and pitch angles work opposite to each other in terms of direction and sign values.

Roll Angle=Old Roll Angle- ∆time*gyro_x_value					

Pitch Angle=Old Pitch Angle+ ∆time*gyro_y_value				

After the roll and pitch angles are computed, the angle of tilt/inclination is computed using the formula mentioned below:

Angle of Inclination=  tan^(-1)⁡〖( 〗 √(〖tan〗^2 (Roll_angle)+ 〖tan〗^2 (Pitch_angle)))

## How the Indicator is decided?

The indicator directions are defined as follows:
1.	Roll angle is positive in case of Right Indicator and Left otherwise.
2.  Pitch angle is positive in case of Left Indicator and Right otherwise.
3.  If both the angles are 0, then no indicator is required. (Indicator off)
