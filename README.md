**Today we are taking our first steps with LVGL and SquareLine Studio.**

Last time I started CrowPanel ESP32 C3 and using Arduino IDE 2.3.4 I ran some basic sketches. Let's move on because this CrowPanel can offer us more.

Let's start with:

  1 Set-up our basic needs together with Arduino;

  2 Install LVGL library for Arduino IDE;

  3 Install SquareLine Studio graphics designed tool;

  4 First instructions in SquareLine Studio.



1. The first step is to gather some files in the same directory, and for this please download the ESP32_1.28_Arduino_Demo archive (https://www.elecrow.com/wiki/CrowPanel_ESP32_1.28-inch_Round_Display.html), if you haven't done so yet.
Next go to Examples → LvglWidgets and copy the header and cpp files (CST816D).
Open Arduino IDE and save a simple empty sketch, locate the directory and paste the files above. Also in this directory please create two other directories in which at some point we will save some files from SquareLine Studio (I called them "square line files" and "ui files" from the user interface).

![Untitled 2](https://github.com/user-attachments/assets/c10afc3c-6dce-484a-9b07-5d4ceec9d4e3)

2. The next thing is to install the Lvgl library in the Arduino IDE (I've already shown how to install a library, but it's nothing special, I'm sure you can do it): https://www.arduinolibraries.info/libraries/lvgl .
LVGL (Lightweight Versatile Graphics Library) is an open-source library used to create graphical interfaces on embedded devices. The library works on most microcontrollers that meet the minimum required resources - 32kB RAM and 128 kB of flash memory. The library also provides dozens of layout examples that can be adapted depending on the use-case.
In a slightly different way I wanted to install Lvgl v8.3.11, you will see later why I did this. Download the archive, and copy the files to "libraries" in the Arduino IDE, make sure they are called "Lvgl".

3. Let's move on to installing a new tool, SquareLine Studio v1.5.0: https://squareline.io/downloads .
A short description provided by the developer goes something like this: "SquareLine Studio is specially developed for designers so as to implement their plans in the most efficient way and to take the most off the programmers' shoulders. SquareLine Studio uses the fully open source LVGL UI library which makes it possible to control the whole project because there is no Lib file generated code set. Meanwhile, it gives great performance on low performance devices. " (https://docs.squareline.io/docs/introduction/overview/)
I suggest you create an account on their website because after you install the program you will need to enter your own license.

4. Now let's open SquareLine Studio and take a few steps.

![Untitled 1](https://github.com/user-attachments/assets/cc710b9b-ebde-455f-9643-9474d3b75751)

If you have successfully installed the tool, when you open it you will be at this point where:

  • we are creating a new project;

  • we are working in the Arduino IDE, so you will select this;

  • we are using the Lvgl v8.3 library;

  • we are also using the TFT_eSPI library (https://docs.arduino.cc/libraries/tft_espi/#Releases).

![Untitled 3](https://github.com/user-attachments/assets/05c8f148-b7f1-4397-b382-a961adfd1714)

On the right side we have:

  • Project Description, I wrote the name of the Arduino sketch;

  • Project name;

  • very important, enter the path to the directory, in this case it is the one called "square line files";

  • Resolution;

  • Shape;

  • Color depth;

  • LVGL version;

  • and finally click on Create button.

And voila:

![Untitled 4](https://github.com/user-attachments/assets/47f22907-5137-4c04-a244-364c071c2cfa) 

It wasn't that hard, was it? But we still have a few settings to make.

![Untitled 5](https://github.com/user-attachments/assets/bae0c8a2-e7bc-41ce-9847-38bde2270b02)

Go to File → Project Settings and in this window check the properties, then in the "File Export" area:

  • "Project Export Root" is the previous path, in my case to the "square line files" directory;

  • "UI Files Export Path" is the path to the other directory, in my case it's "ui files";

  • "LVGL Include Path" actually refers to saving some data in a file, optionally named "lvgl.h" .


![Untitled 6](https://github.com/user-attachments/assets/1241c712-007e-4ebc-b179-4b8bc6284655) 

And finally click on "Apply changes".
So far we are at the same level, I am learning at about the same pace as you. The interface of the tool does not seem complicated to me, so I started to observe what is around. I clicked on some buttons and created a green circle:

![Untitled 7](https://github.com/user-attachments/assets/921961ea-fca0-4e5d-9de4-a102ac56598e) 

Next, I clicked Widgets → Basic → Text Area and inserted some text into the center of my virtual display, then I started customizing it.

![Untitled 8](https://github.com/user-attachments/assets/28a459a0-f310-424f-bcb6-019d17054f1b) 

When you are ready click on Export → Export UI Files which automatically saves the files in your Arduino sketch directory, in my case it is the directory called "ui files".

![Untitled 9](https://github.com/user-attachments/assets/a3102e31-e980-4866-9f09-a36e440de48b)

What do you think, do you like it? What would you create?
Well, we will continue soon. 😉









