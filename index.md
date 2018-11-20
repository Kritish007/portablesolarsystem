# WEEK15
# WEEK14
# WEEK13
# WEEK12
![frontend](https://user-images.githubusercontent.com/42982622/48801619-d8418b80-ecda-11e8-99e1-b1883ea4e5f4.jpg)
![backend](https://user-images.githubusercontent.com/42982622/48801703-0cb54780-ecdb-11e8-939e-ab037ac2cf3d.jpg)
# WEEK11- PCB Power Up Milestone and progress report:

I started testing reading data from my ADS1115 using the code from: http://openlabtools.eng.cam.ac.uk/Resources/Datalog/RPi_ADS1115/code/ADS1115_sample.c

Screenshot of my readings:

![test](https://user-images.githubusercontent.com/42982622/48443290-9f476b00-e75e-11e8-828c-c67c150a8aa5.PNG)
Progress Report:

•	I have my PCB, Raspberry Pi and Solar Panel powered up and receiving readings from my Ads1115 Sensor through Putty. I still need to do a custom laser cut 3d printing case for my project which will include: my PCB, Raspberry Pi where I should have the needed ports for connections visible and my Solar Panel at an appropriate angle to capture enough light.

•	If we look at my Project Schedule, we are in task 5 which I should be rehearsing for presentation and start working on enclosure which is due in Week 12.

•	Financial reports remain intact. No other parts were ordered. It should be around December when I will get together for a meeting with my partner when I will order the NCP1402 5 volts voltage regulator.

•	My plans for next week is to have the case ready and start preparing my project build instruction.

•	However my project differs a little bit from my Proposal. At this moment I just have readings from my Solar Panel. I have not implemented battery and battery charger circuit yet. For the next year project, in order to make the raspberry Pi run on battery instead of AC power supply, I will have to use a Step Up voltage regulator(NCP1402) to give a constant 5 volts from the varying load output from the battery charger circuit. Here is a picture of the battery charger circuit which I am going to use next year also:

![image](https://user-images.githubusercontent.com/42982622/48447745-cd32ac80-e76a-11e8-9222-e90a306d9815.png)


# WEEK10 - PCB Soldered and tested:
At first, my PCB were not giving a full voltage on SCL as the soldering was incomplete on that pin. I resoldered and it worked(i2cdetect -y 1). Testing was also done for my PCB.
![frontpcb](https://user-images.githubusercontent.com/42982622/48170699-9110cf00-e2c6-11e8-8987-0410192c8bbf.jpg)
![backpcb](https://user-images.githubusercontent.com/42982622/48170707-9a9a3700-e2c6-11e8-9e65-0f8f4f284443.jpg)

# WEEK9 - Hardware:
PCB Designed: on fritzing.
![latest_pcb](https://user-images.githubusercontent.com/42982622/48170594-3d05ea80-e2c6-11e8-8011-1853b33bb692.png)

# WEEK8 - Breadboard Milestone and progress report:
![breadboard](https://user-images.githubusercontent.com/42982622/48170806-18f6d900-e2c7-11e8-90bd-214967c04462.jpg)

Progress report:

•	I believe I am 10 days ahead of my Project Schedule. Soldering and power up my ADC1115 testing have been done. 

•	So far, I have already setup my raspberry pi 3b for programming. I have also started to test my ADC1115 with programs which are showing me values for voltage inputs.

•	On the software side, we have already made the backbone of our software application with the layouts but just the functionality needs to be implemented.

•	As concerned on the Financial updates, no other parts have been bought. Budget remains intact. Instead, there are some parts such as: Apex Servo Horn Pack#2, DAC Converter which has not been used in my current project.

•	I encountered an address problem in class when I ran the following command: sudo i2cdetect -y 1 and result came out as address 48. So, I got to know that I need to connect the ADDR to SCL for an address of 0x4B as required.

•	My plan for this week is designing my PCB as I already know what should it contain. I will get my PCB soldered hopefully by next week and testing will be done on the same day.



# WEEK7
Pseudo-Code Assignment due

# WEEK6
STUDY DAYS
# WEEK5 - Proof Of Purchase:
![1](https://user-images.githubusercontent.com/42982622/46377610-0a355a80-c667-11e8-8eae-219a86079d8f.jpg)
![2](https://user-images.githubusercontent.com/42982622/46377611-0a355a80-c667-11e8-9caf-cc08f2a2db3f.jpg)
![3](https://user-images.githubusercontent.com/42982622/46377612-0a355a80-c667-11e8-9c26-09587ed1588b.jpg)
![4](https://user-images.githubusercontent.com/42982622/46377613-0a355a80-c667-11e8-8817-46457f73cb27.jpg)

# WEEK4
Made a Budget Plan for the electronic chips I am going to use
[ProjectBudgetSowamber.xlsx](https://github.com/Kritish007/portablesolarsystem/files/2559887/ProjectBudgetSowamber.xlsx)

# WEEK3
Made a Schedule plan for this semester and the next semester

# WEEK2
Proposal Submission: [CENG 319 Proposal .docx](https://github.com/Kritish007/portablesolarsystem/files/2559888/CENG.319.Proposal.docx)

# WEEK1
Proposed to professor concerning my sensor.

Repository created!
