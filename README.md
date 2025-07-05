Hi everyone! 🙂

Because I have a hobby of creating small, various circuits, I bought an ESP01S (also ESP01) board to use for real-time monitoring of the temperature in the apartment, using a DHT22 and the Blynk application. But first I consulted google to figure out how I can program this MCU using the Arduino IDE. Therefore, I will not present you with anything unknown at all, but there is information that you will also find on the internet.

1. Add the ESP 01/01S board to the Arduino IDE (if it doesn't already exist) by entering the link in the indicated field (Arduino IDE → File → Preferences):
http://arduino.esp8266.com/stable/package_esp8266com_index.json

Put a comma (,) between the others, if there are others (this is my case). Now we have the path needed to install the board.

![image](https://github.com/user-attachments/assets/f13d4902-ce74-4188-8ee2-fdfd3cc63584)

2. Open Tools → Board → Boards Manager and search for "ESP8266", then install the version created by ESP8266 Community.

![image](https://github.com/user-attachments/assets/6b331376-b036-4c7f-8b08-a8e8ce56592d)

![image](https://github.com/user-attachments/assets/2e054dcb-e185-4104-95b8-1c98fc0edd81)

Now we need to know that there are physical differences between ESP01 and ESP01S. 
On the ESP01 the red LED is for power signaling and the blue LED is the "built-in" one that can be controlled by program. 
On the ESP01S we have a blue LED (built-in) that can be controlled by program.

![image](https://github.com/user-attachments/assets/61f37a04-4e69-46be-900b-9a1773c92a0f)
https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.botnroll.com%2Fen%2Fwi-fi%2F5457-esp8266-serial-wifi-module-esp-01s.html&psig=AOvVaw3VPqO89z00mzzQ-GjHTMZI&ust=1749994442788000&source=images&cd=vfe&opi=89978449&ved=0CBcQjhxqFwoTCLCps8GD8Y0DFQAAAAAdAAAAABAE

But the pinout is the same:

![ESP 01 01S Pinout](https://github.com/user-attachments/assets/dfa25538-f6ea-46e3-9ffb-a58e0543b724)
https://www.google.com/url?sa=i&url=https%3A%2F%2Ftheorycircuit.com%2Fbasic%2Fesp8266-based-boards-and-its-pinout-details%2F&psig=AOvVaw2Rr1Fa5UxqQ53JqX3wifwH&ust=1751795785789000&source=images&cd=vfe&opi=89978449&ved=0CBAQjRxqFwoTCLDSypG6pY4DFQAAAAAdAAAAABAE

The diagram below shows how to program the ESP01S using FTDI. Be careful, put the jumper on 3.3V at FTDI, the ESP 01/01S board works at 3.3V.

![image](https://github.com/user-attachments/assets/5e677741-72c0-4af1-9b5e-e4e633ee9fea)
https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.instructables.com%2FFTDI-ESP8266-Definitive-Wiring%2F&psig=AOvVaw3O8pTu-lbvlt2pClbHsHaq&ust=1749994602547000&source=images&cd=vfe&opi=89978449&ved=0CBcQjhxqFwoTCMiLhoqE8Y0DFQAAAAAdAAAAABAE

Also for the ESP01 board:
• FTDI serial converter:
• RX -> TX
• TX -> RX
• Gnd -> Gnd
• CHPD/EN -> 3.3V
• VCC -> 3.3V
• RST -> Button -> Gnd
• GPIO 0 -> Gnd
https://techtalkies.in/2024/02/05/programming-esp-01-in-different-ways/?i=1

Don't forget that in the case of ESP01, after programming, you have to permanently connect CHPD/EN to 3V3. So just powering the board is not enough to make the program run.

My programmer:

![q2](https://github.com/user-attachments/assets/ca6a252a-d7da-4429-8613-0ac33150a052)

![20250614_165827](https://github.com/user-attachments/assets/69918532-a034-4be1-a529-a4abfc387532)

Now, if everything is fine, all you have to do is open the "Blink" sketch and make the LED blink.

<pre>
  <code>  
//You can modifiy the next line if your board has the LED connected to another Pin
#define LED 2 // onboard LED ESP-01S -> Pin 2

void setup() {
  // initialize digital pin LED as an output.
  pinMode(LED, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED, HIGH); // turn the LED on (HIGH is the voltage level)
  delay(1000); // for 1 second
  digitalWrite(LED, LOW); // turn the LED off by making the voltage LOW
  delay(2000); // for 2 seconds
}
  </code>
</pre>  

The ESP01 board is a little bit different, the built-in LED is connected to pin 1 (change it in the sketch above), you still need to select like this:
![image](https://github.com/user-attachments/assets/30e10cb1-699d-4454-b739-6275542983b5)

And here you can also see a short video. 👍

https://youtube.com/shorts/QKwVWmvhdyg?feature=share

#JLCPCB #JLCONE
