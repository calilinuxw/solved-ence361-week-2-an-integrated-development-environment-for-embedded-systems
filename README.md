Download Link: https://assignmentchef.com/product/solved-ence361-week-2-an-integrated-development-environment-for-embedded-systems
<br>
<strong>TI’s Code Composer Studio (CCS)</strong>

This handout for Week-2 is intended for ENCE361 students and complements code and other associated documentation that will be useful to help you complete your embedded systems project. This document outlines a recommended procedure for your second laboratory week and assumes you have either purchased a Tiva Kit (from the CopyCentre) and brought it to the lab, or that you are working with another student who has.

<h1>1.          Laboratory set and group project</h1>




During Weeks 2, 3 and 4 you will have an assortment of laboratory exercises to complete.  These will help you to complete your first Project Milestone in Week 5.

The set of three prescribed laboratories is designed to assist you by providing instruction and exercises on: (i) a professional development environment and commercial toolchain, (ii) familiarisation with several peripheral modules, such as the ADC and accelerometer, and (iii) introduction on the TivaWare API and Orbit BoosterPack display (daughterboard) to help students write C code to complete their development.

<h1>2.         Laboratory books</h1>

Record notes from your labs over Weeks 2 and 5, as well as notes for your project, in an individual lab book. Record in your book which tasks have been completed, results and where you have found information that you needed to complete tasks, e.g. the location of important information in the datasheets and manuals. A soft-covered exercise book, such as a Warwick A4 Exercise book is ideal for this.

<h1>3.       The Tiva LaunchPad &amp; Orbit BoosterPack</h1>

The Tiva LaunchPad is a small, self-contained development board made by Texas Instruments.  The specific board you will be using for this project features the TM4C123GH6PM Cortex-M4 microcontroller (MCU) [1], which supports two user-programmable push-button switches (SW1, SW2), an RGB LED, a number of peripherals (ADC, timers, etc.) and a USB interface. Fitted atop the Tiva is a <em>daughterboard</em> (top printed circuit board) that extends the functionality. This daughterboard is referred to in the literature as an Orbit <em>BoosterPack</em>, and supports a digital display and potentiometer that you will use in future weeks.

Documentation on the TM4C123 microprocessor and the Code Composer Studio (CCS) toolchain, in addition to application notes and errata, can be found on your course <u>Learn</u> pages.

<h1>4.              .  Learning  Outcomes</h1>

<ul>

 <li>Develop confidence to build and modify a simple microprocessor application.</li>

 <li>Use a debugger to help find and correct programming faults.</li>

</ul>

<strong>Your objective this week</strong>: <em>Understand the fundamentals of Code Composer Studio and locate and use API functions to help you modify provided C code using the GPIO peripheral.</em>

<strong>           </strong>

<h1>5.     Recommended Procedure</h1>

<strong> </strong>

<h2>5.1.            CCS Tutorial</h2>

In the <em>Projects and Laboratories</em> page on the ENCE361 Learn site you will find a folder, <em>Week-2</em>, containing a PDF tutorial for Code Composer Studio: <strong>CCS 9_2_0 Tutorial.pdf</strong><em>. </em>Closely carry out the procedures outlined in this tutorial. <strong>NB</strong>: It is important to keep the same directory structure throughout your lab work. In later labs you will be able to define your own project directory but for now, follow the instructions. Completion of this tutorial should take between 30 and 50 minutes.




<h2>5.2.            Analysing the source code – week2_blink.c</h2>

After building your first CCS project you should study the source code. Find and study the main function in <em>week2_blink.c</em>, which can be downloaded from the <em>Laboratory source code</em> folder on the <em>Projects and Laboratories</em> page on Learn. Note how variables are defined. We recommend using the unsigned integer types, such as <strong>uint8_t, uint32_t</strong>, etc., similar to what was used in ENCE260, <strong>not </strong>the standard C language types, e.g. unsigned.  These definitions are in <em>stdint.h.</em>

As with most embedded systems programming, there are a number of initialization tasks to perform.  Your first programs in this course will have more lines of code associated with initialization than for anything else!  In particular, note the API<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> functions that are called. The documentation that defines API functions used with the Tiva can be found in two documents:

<ol>

 <li><em>Tiva Launchpad User Guide</em>, [2] and,</li>

 <li><em>TivaWare Peripheral Library User Guide</em> [3] (API function guide)</li>

</ol>




As you progress, you will find the following document also useful:

<ol start="3">

 <li><em>Orbit BoosterPack Reference Manual</em> [4].</li>

</ol>




These are on the <em>Data Sheets and Manuals</em> page on Learn. The <em>Launchpad User Guide</em> defines hardware resources supported on your Tiva board (like switch button details). The <em>Peripheral Library User Guide</em> defines API functions for your MCU peripherals, such as analogue-to-digital converter (ADC), timers, GPIO, etc. The <em>Orbit BoosterPack Reference Manual </em>outlines the electrical connections and port addresses for you OLED display. <u>You will routinely need to</u> <u>consult these documents as well as the processor datasheet [1] from now on</u>.




<h2>5.3.            Running the initial source code – week2_blink.c</h2>




Currently, the only purpose of the <em>week2_blink.c</em> program is to flash the LED on the Tiva board. Thus, it is a relatively simple program.

<strong> </strong>

As outlined in the CCS tutorial guide that you completed before starting this part of the lab, add a new project to your existing workspace and call this Week2_Lab. Copy the <em>week2-blink.c</em> source from Learn into your project directory. Set up the compiler and linker settings, identical to that outlined in the CCS tutorial. After completing this, your program should compile, link and load into your Tiva board. Push the green ‘execute’ arrow to start it running.  Refer to the CCS tutorial guide if you get stuck.




<h2>5.4.            Modifying the code</h2>

For this lab you are required to modify the source code so that the blinking of the LED will only occur once you press the pushbutton switch SW1, and continue only while pushbutton SW1 is pressed. Sound familiar? Well, you have to start somewhere!  There is plenty of scope for making more interesting mods, if you have the time and inclination.




<strong>Important:  </strong>Rather than change the code within the same file, make a new copy and rename it; make your changes in the new file.  This is a simple form of source control; once your group’s <strong>git </strong>repository is established, get into the habit of using it for your group’s source file control.




Once you have more than one *.c file in your project, the compiler needs to know which to compile (it knows that there should only be a single <strong>main()</strong>):  To fix this, exclude the original file from your build: right-click over the file name in the Project Explorer window and Exclude from Build.  Of course, as your code base grows, other .c files may be required that do need to be in the build.




Look through the <em>Tiva Launchpad User Guide</em> (<em>UG</em>) for port labels used in your program to initialize SW1 as an input, just after, for example, line 44. Once you determine the appropriate port letter, e.g., E, F, or G, and the specific pin number on that 8-bit port, use an appropriate GPIO pin function to set this port pin as an input, and secondly, configure the specific GPIO pin to draw 4 mA through the internal pull-up (remember what these are?). Lastly, around Line 64, write a simple <strong>if</strong> construct that tests the port pin, such that the LED only blinks as long as switch SW1 is pressed.




<h1>6.  Further program development, debugging and testing</h1>




As mentioned, TivaWare is an API library and it is intended to help make programming easier by effectively using pre-written functions. The Texas Instruments compiler (based on <strong>gcc</strong>) has been installed on the hard disk drive of each PC host in the Electronics Lab. Similar to the AVR compiler you used in ENCE260, this program compiles and links ARM code. When built, the resulting ELF binary file can be downloaded to your Tiva board by selecting the debug icon. An in-circuit debugger is integrated within CCS and this can be used to test and debug software. For example, set a breakpoint just after the variable <strong>clock_rate</strong> is assigned a value. Do this by double clicking on the blue region on the extreme left within your source code window. A blue icon should appear on the left of the line of source you clicked on to show the breakpoint. Next, set up a watch expression or variable for <strong>clock_rate</strong>. Run your debugger to a breakpoint that you have set just past your <strong>clock_rate</strong> variable declaration. Note the value for <strong>clock_rate</strong>. Does this value agree with your expectation?




Now, experiment by altering the code in other ways, recompile and load the program, and test the result. Suggestions include:




<ol>

 <li>See if you can use different colour LEDs for your display.</li>

</ol>




<ol>

 <li>Look at the setup used for the CPU clock. Once set up, note that SysCtlDelay(arg) uses a magic number (yes, you can improve on this code) in calculating the parameter. What is the original blink rate? – this can be found without testing. If you increase this number will the flash period be extended or will it reduce?  Hint: Refer to SysCtlDelay(arg) in the <em>TivaWare Peripheral Driver Library</em> (use search in the PDF) to find what this function does and the relationship to arg. Why is it written in assembler?</li>

</ol>




<ol>

 <li>Can you explain the warning given in the TivaWare peripheral library user guide for the application of SysCtlDelay()?</li>

</ol>




<ol>

 <li>What is the duty cycle of the LED flasher? What code modifications are needed to change this to, say, a duty cycle of 20%? Considering what you now know about SysCtlDelay(), calculate two argument expressions to achieve a duty cycle of 20% while the blink rate stays the same.</li>

</ol>







<h1>7.   References</h1>




[1] <em>Tiva TM4C123GH6PM microcontroller datasheet</em>, Texas Instruments, SPMS376E, 2014   [2] <em>Tiva C Series TM4C123G LaunchPad Evaluation board</em>, Texas Instruments, SPMU296,

2013.

<ul>

 <li><em>TivaWare Peripheral Driver Library User’s Guide</em>, Texas Instruments, SPMU298D, 2016.</li>

 <li><em>Orbit Boosterpack Reference Manual</em>, Digilent Inc., DOC# 6032-502-000, 2013.</li>

</ul>




<strong> </strong>

<a href="#_ftnref1" name="_ftn1">[1]</a> Application Programming Interface