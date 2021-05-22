# Designing Electric Vehicle Powertrain Using Matlab/Simulink Platform
## Overview and key terms:
For being ecofriendly and driven by renewable energies Electric Vehicle (EV) is becoming very popular day by day. 
Before constructing a practical vehicle, modeling and simulating the design is very important to find out the pros and
cons of the design. In this project modeling of a simple EV powertrain is made and how the vehicle drive can be 
improved by using a higher rated motor is shown. A block diagram representing the modeling in brief shown below:
![image](https://user-images.githubusercontent.com/72512233/119240345-be65b580-bb70-11eb-8fb6-1fd04d2f9caa.png)

Fig 1. Block diagram to represent EV model
### Vehicle body:
The first step of modeling a vehicle is modeling vehicle body. Vehicle body is composed mainly of 4 wheels, chassis and gearbox. In the Simulink platform, a subsystem is made representing vehicle body. The vehicle body subsystem comprises of four wheels, gearbox and vehicle body block. Four wheels are connected by hubs to the body. The rotational part to be connected to the gear box. Gear ratio of 3.7 is used here. Power to be delivered to the rear wheels only. From the vehicle body block, output of vehicle speed can be achieved. Wind velocity and slop of the inclined road are given as input to the vehicle body. Weight of the vehicle is another parameter of the vehicle body. It can be shown that using a light weight vehicle, vehicle control can be much easier. But as mainly electrical components are analyzed in this project so the weight of the vehicle is left out as constant 400kg. Thus, a very simple vehicle body was designed.

### Motor:
Motor is the heart of electric powertrain system. Different kinds of motor are being used now a days for EV. For example- DC motors, Induction motor, Synchronous motor, Reluctance motor and so on. For simplicity, a permanent magnet brush DC motor is being used here. Changing motor type may make significant difference in the output. A comparison had been made changing motor ratings in the later part of the project.

### Battery:
Battery stores the required power to drive the vehicle. In modern EVs, lithium ion battery is used. Battery and battery management system is a more complicated study. Here a simple battery cell is being used to have the output of current flow through the vehicle.
While measuring the current flown through the vehicle, it was seen that there are many a time current measure was negative. This was because of regenerative braking system. During this period of time, instead of suppling power to the vehicle, battery becomes charged using surplus rotation of the motor. For that moment of time motor acts as a dynamo and battery gets charged. 

### Power converter:
To control velocity of a vehicle, supply from the battery is to be controlled and thus, speed of the motor can be controlled. This is done by power converter. H-bridge converter pairing up with a PWM module was used in this simulation. The PWM module takes up the signal form the driver and then ask H-bridge to act accordingly. 
Here to note that, there are two modes in Simulink, these two blocks can be set up. One is in “PWM” mode and the other is “Averaged” mode. In “PWM” mode, both of them operates in exact timing consuming a lot of time during simulation. But this mode shows more precise output. On the other hand, in “Averaged” mode, average values of the PWM are taken and simulate the system in a much less time sacrificing precision of the output. As everything is being simplified here, simulation of this design was done in “Averaged” mode making a faster simulation.  
These motor, battery, H-bridge converter and PWM module were merged into a new subsystem named as Motor Drive.

### Driver controller: 
Driver controller block represents a vehicle driver inside the vehicle. As per the drive cycle suggests, the “Longitudinal Driver” block accelerates and retards the speed of the vehicle. The Acceleration Command or “AccelCmd” port gives the necessary acceleration signal to the PWM. And “DecelCmd” port delivers brake pedal action to the brake (BRK) port of the H-bridge. Output of the “AccelCmd” is shown in the report to compare the timing of acceleration command with final speed.
In the “Longitudinal Driver” block there is a feed back input port. This input port feed the speed of the vehicle back to the block to compare the expected speed vs final speed and then, the block works accordingly.

### Drive cycle:
To simulate and analysis the vehicle design, a drive cycle is necessary. Drive cycle represents the practical speed changes a vehicle may make during practical use. For example, driving a vehicle in a rural road may have to change velocity more frequently than driving in urban roads. Simply, a drive cycle is an accumulation of expected speed of the vehicle at respective time. “ECE R15 (single cycle)” of a time period of 195 seconds is being used here. This drive cycle was downloaded from official website of Matlab.

![image](https://user-images.githubusercontent.com/72512233/119240034-0c79b980-bb6f-11eb-9617-2faa106cfdb1.png)

Fig 2. Drive cycle that was used for this project

## Circuit setup for Simulink simulation:
###	Vehicle Body (Subsystem):
![image](https://user-images.githubusercontent.com/72512233/119240080-624e6180-bb6f-11eb-9589-fdf2c17f5d18.png)

Fig 3. “Vehicle Body” subsystem for EV vehicle modeling
### Motor Drive (Subsystem):
![image](https://user-images.githubusercontent.com/72512233/119240107-88740180-bb6f-11eb-923b-b66ff8363a1e.png)

Fig 4. “Motor Drive” subsystem for EV vehicle modeling
###	Complete EV Powertrain:
![image](https://user-images.githubusercontent.com/72512233/119240112-932e9680-bb6f-11eb-9f64-e4149ce1e7c8.png)

Fig 5. Complete diagram of EV powertrain combining the subsystems 

## Simulation 1:
### Motor parameters: 
1.	No-load speed: 8000 rpm
2.	Rated speed (at rated load): 6000 rpm
3.	Rated load: 50 kW
4.	Rated DC supply voltage: 300V
### Acceleration pedal signal:
![image](https://user-images.githubusercontent.com/72512233/119240133-b22d2880-bb6f-11eb-9f01-755e3d34b5e9.png)

Fig 6. Acceleration pedal signal vs time plot for simulation 1
### Current flow measurement:
![image](https://user-images.githubusercontent.com/72512233/119240180-e6a0e480-bb6f-11eb-8c79-1a477fc56f4c.png)

Fig 7. Current flow through the vehicle during simulation
###	Comparison between expected and final output speed:
![image](https://user-images.githubusercontent.com/72512233/119240195-f5879700-bb6f-11eb-971e-342b1c9143d6.png)

Fig 8. Comparison between expected speed and achieved speed with respect to time

## Simulation 2:
### Motor parameters:
1.	No-load speed: 10000 rpm
2.	Rated speed (at rated load): 8000 rpm
3.	Rated load: 100 kW
4.	Rated DC supply voltage: 500V
### Acceleration pedal signal:
![image](https://user-images.githubusercontent.com/72512233/119240237-28ca2600-bb70-11eb-94ce-57946d5dc696.png)

Fig 9. Acceleration pedal signal vs time plot for simulation 2
### Current flow measurement:
![image](https://user-images.githubusercontent.com/72512233/119240244-37184200-bb70-11eb-9f3c-0ac5049a0282.png)

Fig 10. Current flow through the vehicle during simulation
### Comparison between expected and final output speed:
![image](https://user-images.githubusercontent.com/72512233/119240259-48614e80-bb70-11eb-8f09-137dea415ea7.png)

Fig 11. Comparison between expected speed and achieved speed with respect to time

## Conclusion:
If both the outputs are compared, it can be clearly seen that, by using a higher rated motor final speed output becomes more precise. But higher rated motor would cost more and would have more weight. But weight was kept constant here. So, taking all the changes and factors into account, an EV designer would design the vehicle. Moreover, the negative current flow suggests that, sometimes instead of flowing from the battery, current flows to the battery. And by this way regenerative braking works. As a whole, a brief and very basic idea to design an Electric Vehicle was demonstrated in the project.  


