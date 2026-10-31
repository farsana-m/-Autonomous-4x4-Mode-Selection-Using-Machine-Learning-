 Autonomous 4x4 Mode Selection Using Machine Learning

1. Project Overview

Machine Learning-Based Automatic Drivetrain Mode Selection is a MATLAB/Simulink-based project that explores the automatic selection of vehicle drivetrain modes using machine learning.
The system predicts a suitable drivetrain mode based on vehicle operating conditions instead of relying entirely on manual driver selection.
The three drivetrain modes considered are:

2H (Two-Wheel Drive – High Range): Used for normal driving conditions.
4H (Four-Wheel Drive – High Range):Used when additional traction is required.
4L (Four-Wheel Drive – Low Range):Used for low-speed driving conditions requiring higher wheel torque.
The project demonstrates an ML-based approach to automatic drivetrain mode selection in an SDV-oriented architecture.

2. Project Objectives

- Develop an automatic drivetrain mode-selection system.
- Use vehicle operating parameters as inputs to a machine learning classifier.
- Predict one of three drivetrain modes: 2H, 4H, or 4L.
- Integrate the ML prediction with a functional transfer-case simulation.
- Evaluate the system under different simulated road and driving conditions.

3. System Architecture

The project follows this general processing flow:
1. Vehicle dynamics simulation generates vehicle operating data.
2. Wheel-speed signals are collected for all four wheels.
3. Wheel-slip values are calculated.
4. Vehicle speed and road-friction scenario information are used as additional inputs.
5. The input features are supplied to the trained machine learning model.
6. The classifier predicts the appropriate drivetrain mode.
7. The transfer-case subsystem applies the corresponding simulated drivetrain configuration.

Architecture Flow


       Vehicle Dynamics Model
                 |
                 v
       Vehicle Operating Signals
                 |
       +---------+----------+
       |                    |
  Vehicle Speed       Wheel Speeds
                            |
                            v
                      Wheel Slip
                            |
                            v
                 Feature Preparation
                            |
                            v
                 ML Mode Predictor
                            |
                            v
                 Predicted Mode
                    /    |    \
                  2H    4H    4L
                    \    |    /
                            |
                            v
                  Transfer Case Model
                            |
                            v
                 Simulated Wheel Torque

4. Machine Learning Input Features

The classifier uses the following ten input features:
 1  VehicleSpeed_kmh 
 2  WheelSpeed_FL 
 3  WheelSpeed_FR 
 4  WheelSpeed_RL 
 5  WheelSpeed_RR 
 6  Slip_FL 
 7  Slip_FR 
 8  Slip_RL 
 9  Slip_RR 
 10 RoadFrictionFactor 

ML output classes:

 Class  Predicted Mode 

 1      2H 
 2      4H 
 3      4L 

The road-friction factor is a simulated scenario input, not a direct measurement from a physical friction sensor.

5. Technologies Used

- MATLAB
- Simulink
- MATLAB Statistics and Machine Learning Toolbox
- Vehicle dynamics simulation
- Classification Decision Tree
- Machine learning-based mode prediction

6. How to Run the Project

Before running the project, ensure that you have:

- MATLAB installed.
- Simulink installed.
- Statistics and Machine Learning Toolbox installed.
- The project Simulink model and its required supporting files.

Step 1: Download the Repository

Clone the repository using Git:
git clone https://github.com/farsana-m/-Autonomous-4x4-Mode-Selection-Using-Machine-Learning-.git

Step 2: Open MATLAB

Open MATLAB and navigate to the extracted project folder.
Set the project folder as the current working directory.

Step 3: Initialize the Workspace

The simulation requires the vehicle model parameters and trained ML model variables.
If the saved workspace file is available, load it:

>>load('Autonomous4x4_ML_Workspace.mat');

Initialize the vehicle model parameters:

>>sldemo_absdata;
>>m_vehicle = m;

If you do not have the saved workspace file, the required model variables and trained classifier must first be generated or loaded from their respective project files.

Step 4: Open the Simulink Model

>>open_system('Autonomous_4x4_ML_Control');

The top-level Simulink model contains the vehicle dynamics, ML mode predictor, and transfer-case simulation.

Step 5: Run the Simulation

Test Case 1 – 2H Mode

>>v0 = 12;
>>RoadFrictionFactor = 1.0;
>>sim('Autonomous_4x4_ML_Control');

Test Case 2 – 4H Mode

>>v0 = 12;
>>RoadFrictionFactor = 0.4;
>>sim('Autonomous_4x4_ML_Control');

Test Case 3 – 4L Mode

>>v0 = 4;
>>RoadFrictionFactor = 0.25;
>>sim('Autonomous_4x4_ML_Control');

7. Simulation Output
   
The system demonstrates:
- Vehicle operating parameter monitoring.
- Wheel-speed and wheel-slip evaluation.
- ML-based drivetrain mode prediction.
- Automatic selection among 2H, 4H, and 4L.
- Simulated transfer-case configuration.
- Corresponding simulated wheel-torque outputs.

The transfer-case torque distribution and low-range multiplication used in this model are simulation assumptions, not universal vehicle specifications.

8. Current Project Scope and Limitations

This project is currently a software-based MATLAB/Simulink simulation prototype.
- No physical vehicle hardware or transfer-case actuator is connected.
- Vehicle operating conditions are generated through simulation.
- Road friction is represented by a controlled simulation parameter.
- The ML training labels are generated using experimental rule-based conditions.
- The results demonstrate the feasibility of the proposed approach within the simulated environment.

Real-vehicle implementation, ECU integration, actuator control, hardware-in-the-loop testing, and vehicle validation are proposed future development activities.

9. Future Scope

- Integration with an automotive ECU or domain controller.
- Development of a real-time mode-selection function.
- Integration with an electric transfer-case shift actuator.
- Hardware-in-the-loop testing.
- Validation using real vehicle operating data.
- Safety monitoring and secure communication.
