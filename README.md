# portablesolarsystem
### Table of Contents
1.  [Introduction](#Introduction-using-a-system-diagram)
2.  [Bill of Materials/Budget](#Bill-of-Materials) 
3.  [Time Commitment](#Time-Commitment)
4.  [Mechanical Assembly](#Mechanical-Assembly)
5.  [PCB/Soldering](#PCB-Soldering)
6.  [Power Up](#Power-Up)
7.  [Unit Testing](#Unit-Testing)
8.  [Production Testing](#Production-Testing)
# Introduction using a system diagram
![system design](https://user-images.githubusercontent.com/42982622/49830478-453ac500-fd5f-11e8-8344-6b2f8369185e.png)
This is my sensor which I used: <br/>
![ads1115](https://user-images.githubusercontent.com/42982622/49827298-fa1cb400-fd56-11e8-92e4-277b1a9c7a47.png)
Picture was cropped from: https://www.adafruit.com/product/1085 <br/>

Please be aware that my sensor is hidden under the large Pi Cobbler cable. <br/>
![front](https://user-images.githubusercontent.com/42982622/49824300-cdb16980-fd4f-11e8-898e-ef7c0ce9466d.jpg)
![back](https://user-images.githubusercontent.com/42982622/49824316-d30eb400-fd4f-11e8-99d3-79dec2b79726.jpg)


Concerning software, in order to use ssh connection to my raspberry pi, I had to enable ssh and install xrdp on my raspberry pi before I could get connected. Moreover, I had to install gnu/c compiler as the program I used is in c. Also, from the windows, I had to go to Network and sharing center where I had to go to properties/sharing, ticked the: allow other network users to connect through this computer's internet connection and selected Ethernet from the drop down list. <br/>



# Bill of Materials
These are the following components I have used for this semester: <br/>
Mini encapsulated solar cell Epoxy $14 <br/>
Raspberry Pi 3 Kit $113 <br/>
ADS1115 16Bit ADC $15 <br/>
Pi cobbler $20 <br/>

Here is a picture of where I purchased the components : <br/>
![1](https://user-images.githubusercontent.com/42982622/46377610-0a355a80-c667-11e8-8eae-219a86079d8f.jpg)
![2](https://user-images.githubusercontent.com/42982622/46377611-0a355a80-c667-11e8-9caf-cc08f2a2db3f.jpg)
![3](https://user-images.githubusercontent.com/42982622/46377612-0a355a80-c667-11e8-9c26-09587ed1588b.jpg)
![4](https://user-images.githubusercontent.com/42982622/46377613-0a355a80-c667-11e8-8817-46457f73cb27.jpg)

Printed Circuit Board, 10 pins socket, customized acrylic casing and other needed utilities were provided by the Prototype Lab. <br/>
The plan for next semester is to use the following already purchased components except for the last component: <br/>
Polymer Charger $19 <br/>
Lithium Polymer Battery $16 <br/> 
Male DC Power Adapter $4  <br/>
NCP1402 5 volts voltage regulator $7 (STILL NEEDS TO PURCHASE) <br/>

# Time Commitment
![timecommitment](https://user-images.githubusercontent.com/42982622/49824569-65af5300-fd50-11e8-90a7-5e976da4524b.png)
Even though I have stated it would take me 15 weeks to fully complete this project with its instruction, the project can be fresh started and be finished within 7 weeks. The parts ordered, PCB printing and PCB soldering plays a major part in completion of the project. <br/>

# Mechanical Assembly
A change of address from 0x48 to 0x4B was required. This was done by connecting the ADDR to the SCL pin. <br/>
The ads1115 was connected to a 10 pin header which was soldered on the pcb. In addition, as you can see, I have soldered my pi Cobbler also to the PCB. There is also a pair of 10K resistors which is working to divide the voltage from the solar panel and to my sensor. This is done to avoid burning my sensor as it is recommended to measure a voltage of less than 3.3v. <br/>
After receiving my case, I had to glue the front end of the case to the back end of the case including its 'holder' which will hold the solar panel. I had to use 2 screws to hold the broadcom development platform, 2 screws for holding the pcb with all the components already soldered to it. At the top of the panel, I used a small piece of plastic and a screw to hold the panel firm.

# PCB Soldering
For designing the printed circuit board, I have made use of the software Fritzing as it is a user friendly software to help design and print my pcb. The printed pcb required Gerber files which the printing maching will recognise. <br/>
Please follow the soldering instructions and safety before soldering your pcb. Remember to wear the safety glass. <br/>
This is how my PCB looks after soldering: <br/>
![frontpcb](https://user-images.githubusercontent.com/42982622/49824367-ec176500-fd4f-11e8-8703-3669a34bdb7f.jpg)
![backpcb](https://user-images.githubusercontent.com/42982622/49824368-ec176500-fd4f-11e8-8948-25bf8d5d45ef.jpg)

# Power Up
![poweruptesting](https://user-images.githubusercontent.com/42982622/49824351-e457c080-fd4f-11e8-9f5e-c7b8d0077b0d.png) <br/>
From my code below, you can see I have multipled the receiving result by 2.048 as it is covering the job of the resistors. The resistors basically divides the voltage by 2. I have multiplied by 2 to give a reliable result. <br/>

```ads1115.c```
```
/* 
	ADS1115_sample.c - 12/9/2013. Written by David Purdie as part of the openlabtools initiative
	Initiates and reads a single sample from the ADS1115 (without error handling)
*/

#include <stdio.h>
#include <fcntl.h>// open
#include <inttypes.h>  // uint8_t, etc
#include <linux/i2c-dev.h> // I2C bus definitions
#include <unistd.h>

int main() {
	
  int ADS_address = 0x4B;	// Address of our device on the I2C bus
  int I2CFile;
  
  uint8_t writeBuf[3];		// Buffer to store the 3 bytes that we write to the I2C device
  uint8_t readBuf[2];		// 2 byte buffer to store the data read from the I2C device
  
  int16_t val;				// Stores the 16 bit value of our ADC conversion
  
  I2CFile = open("/dev/i2c-1", O_RDWR);		// Open the I2C device
  ioctl(I2CFile, I2C_SLAVE, ADS_address);   // Specify the address of the I2C Slave to communicate with

while(1){	  
  // These three bytes are written to the ADS1115 to set the config register and start a conversion 
  writeBuf[0] = 1;			// This sets the pointer register so that the following two bytes write to the config register
  writeBuf[1] = 0xC3;   	// This sets the 8 MSBs of the config register (bits 15-8) to 11000011
  writeBuf[2] = 0x03;  		// This sets the 8 LSBs of the config register (bits 7-0) to 00000011
  
  // Initialize the buffer used to read data from the ADS1115 to 0
  readBuf[0]= 0;		
  readBuf[1]= 0;
	  
  // Write writeBuf to the ADS1115, the 3 specifies the number of bytes we are writing,
  // this begins a single conversion
  write(I2CFile, writeBuf, 3);	

  // Wait for the conversion to complete, this requires bit 15 to change from 0->1
  while ((readBuf[0] & 0x80) == 0)	// readBuf[0] contains 8 MSBs of config register, AND with 10000000 to select bit 15
  {
	  read(I2CFile, readBuf, 2);	// Read the config register into readBuf
  }

  writeBuf[0] = 0;					// Set pointer register to 0 to read from the conversion register
  write(I2CFile, writeBuf, 1);
  
  read(I2CFile, readBuf, 2);		// Read the contents of the conversion register into readBuf
  val = readBuf[0] << 8 | readBuf[1];	// Combine the two bytes of readBuf into a single 16 bit result 
  //Edited part
  float voltage = (((float)val*4.096/32767.0)*2.048);
  if(voltage < 1.29){
  printf("Default 0v/Not connected\n");
  sleep(1.5); //sleep for 1.5 seconds
			}
else{
  printf("Voltage Reading %.2f (V) \n", voltage);	// Print the result to terminal, first convert from binary value to mV		
  sleep(2.5); //sleep for 2.5 seconds
}
}
  close(I2CFile);
  return 0;

}
```

# Unit Testing
![assemble](https://user-images.githubusercontent.com/42982622/49825234-ede22800-fd51-11e8-8b8d-6abb57f44af8.jpg)
![i2cdetect](https://user-images.githubusercontent.com/42982622/49824587-6d6ef780-fd50-11e8-9925-e4cbc1b9c42a.png)
To test if my sensor is working, I have to ensure the following connection is done: <br/>
1. VCC is connected to 3.3v to my pi Cobbler board <br/>
2. GND is connected to GND to my pi Cobbler board <br/>
3. SCL is connected to SCL to my pi Cobbler board <br/>
4. SDA is connected to SDA to my pi Cobbler board <br/>
5. Test: sudo i2cdetect -y 1 <br/>

# Production Testing
From the acrylic case I made, there could be a little modification to resize the overall project into a smaller and very particular case. The pi Cobbler could be bypassed, but then the connections will have to be direct to the raspberry pi. This would minus a $20 from the budget. If the same project is being manufactured in big quantity, the soldering process can be done through machine to speed up the process. Also, a mass testing of the project can be done by connecting every single one to Wi-Fi, and connecting to them through remote desktop connection.

This would require a working time between 3-8 weeks depending on the required parts to arrive within the time frame. In general, the project is reproducible by following this instruction. It might need a little of more knowledge about setting up raspberry pi, remote desktop connection and safely power off the project. Please refer to the following websites if you encounter problem while setting up the components: <br/>
https://learn.adafruit.com/adafruit-4-channel-adc-breakouts/assembly-and-wiring
