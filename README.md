Hello makers!

This is the board from DFRobot called Beetle ESP32-C6, a real coin size board:


![94a6cfae52fad3dc8896f1760ea6adb8](https://github.com/user-attachments/assets/d1e970e9-4984-4ea9-bf9d-64b3e5a6374a)


![51ab86bba659126748111cb59bb4b12a](https://github.com/user-attachments/assets/f0609c4e-dc5f-4207-afd3-54aaf112a125)


![20250406_125345](https://github.com/user-attachments/assets/6092a755-6e5b-4aeb-83d6-145e701ca79e)


![20250406_125355](https://github.com/user-attachments/assets/d2e450b3-999a-45ce-b3a3-ecac13aa1f37)

More details can be found by accessing the links:

https://wiki.dfrobot.com/SKU_DFR1117_Beetle_ESP32_C6 

https://youtube.com/shorts/LE2zEx3rlVk?feature=share

https://youtube.com/shorts/NmfaLIAVBrw?feature=share

In the first link you will find how to install Beetle ESP-C6 in Arduino IDE, the steps are few and easy to follow, thank you DFRobot for these, and in the following links you will see what I did for the beginning to use this board.

Using KiCAD I built an expansion board that would allow me access to GPIO and which I prepared for a common application, for example monitoring using various environmental sensors and possibly a display either LCD, OLED or matrix. I also placed a generic power jack, a DC jack, I thought that the main power source for the entire circuit would be 5V, many modules work at this voltage. As for programming, you take out the ESP32-C6, program it with Arduino IDE for example, connect your parts to the expansion board, mount the ESP-C6 and enjoy what you created.
The PCB is single layer, 48*54mm in size and uses through hole components so it is easy to assemble manually. And the circuit:

![_blank](https://github.com/user-attachments/assets/463b7cfa-7d60-409a-a3aa-7ef41d3e792f)

![20250406_125157](https://github.com/user-attachments/assets/cfc75786-bf7d-4ccc-8926-f2de1bf23626)

![Beetle WS2812 Panel](https://github.com/user-attachments/assets/066b4a9d-ac64-4a05-9e33-b5f0a0a114cb)

![20250513_182708](https://github.com/user-attachments/assets/e9c5a380-ca1d-4fae-9596-abe14902e37d)

![20250513_182739](https://github.com/user-attachments/assets/decf5761-a0f6-4565-920f-ac44ba4fd21d)

If you want to see a few simple projects using this board then just go back to the main page.




