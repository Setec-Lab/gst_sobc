Secondary Onboard Computer for SETECLab's Ground Station Terminal  
============

### Most recent version of this repository can be found in: ###

* [GitHub](https://github.com/Setec-Lab/gst_sobc)

### What is this repository for? ###

* This repository was created to develop an SOBC for the SETECLab's custom GST. 

### MSP432 information

* [Datasheet](https://www.ti.com/lit/ds/slas826h/slas826h.pdf?ts=1602367336655&ref_url=https%253A%252F%252Fwww.ti.com%252Ftool%252FMSP-EXP432P401R)
* [Development board: MSP432 LaunchPad](http://www.ti.com/tool/MSP-EXP432P401R)
* [Programmer when integrated in the PCB: OLIMEX MSPBSL](https://www.ti.com/tool/MSPBSL) 

### How do I get set up? ###

* Remove **5V jumper** (**J101** jumper bench) on [MSP432 LaunchPad](http://www.ti.com/tool/MSP-EXP432P401R) (Important! Otherwise, two 5V sources will feed the 5V power line on the PCB)
* Connect [MSP432 LaunchPad](http://www.ti.com/tool/MSP-EXP432P401R) to PC via USB
* Compile with [Code Composer Studio](http://www.ti.com/tool/CCSTUDIO) (Build Project) and Run-->Debug


## Known issues
* Current tests have shown that the **SPI frequency** is somehow band-pass limited: The frequency must be above 70 kHz and below 3 MHz for a proper functioning SPI communication between MSP432 and PIC16. Though, this phenomen might be due to the fact that for testing the SPI communication, a voltage level shifter consisting of _74LS245N_ and _CD4050BE_ has been used which might be a limiting factor. However, using **400 kHz SPI clock speed** is a reasonable and sufficient fast frequency.

### Contribution guidelines ###

* If you want to propose a review or need to modify the code for any reason first clone this [repository](https://github.com/Setec-Lab/gst_pobc) in your PC and create a new branch for your changes. Once your changes are complete and fully tested create a pull request.
* If you just want to do local changes instead you can download a zip version of the repository and do all changes locally in your PC. 

### Who do I talk to? ###

* [Juan J. Rojas](mailto:juan.rojas@itcr.ac.cr)
* [Jean P. Jimenez](mailto:@gmail.com)

 