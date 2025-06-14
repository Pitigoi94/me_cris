Hi everyone! 🙂

Because I have a hobby of creating small, various circuits, I bought an ESP01S board to use for real-time monitoring of the temperature in the apartment, using a DHT22 and the Blynk application. But first I consulted google to figure out how I can program this MCU using the Arduino IDE.
Therefore, I will not present you with anything unique at all, but there is information that you will also find on the internet.

1. Add the ESP01S board to the Arduino IDE (if it doesn't already exist) by entering the link in the indicated field (Arduino IDE → File → Preferences):

http://arduino.esp8266.com/stable/package_esp8266com_index.json

Put a comma (,) between the others, if there are others (this is my case).
Now we have the path needed to install the board.

![image](https://github.com/user-attachments/assets/3545c527-afc7-4de3-b92a-3672827bf4f6)


2. Open Tools → Board → Boards Manager and search for "ESP8266", then install the version created by ESP8266 Community.

![image](https://github.com/user-attachments/assets/c90fd71a-df71-4a12-9510-9dccb04a00e0)

![image](https://github.com/user-attachments/assets/2a9c504b-610e-4211-bfaa-1c2ec6ca6b5f)

Now we need to know that there are differences between ESP01 and ESP01S.

![image](https://github.com/user-attachments/assets/2f6edd02-cf0c-4744-9ba9-e08844004d3c)
https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.botnroll.com%2Fen%2Fwi-fi%2F5457-esp8266-serial-wifi-module-esp-01s.html&psig=AOvVaw3VPqO89z00mzzQ-GjHTMZI&ust=1749994442788000&source=images&cd=vfe&opi=89978449&ved=0CBcQjhxqFwoTCLCps8GD8Y0DFQAAAAAdAAAAABAE 

The diagram below shows how to program the board using FTDI. Be careful, put the jumper on 3.3V at FTDI, the ESP01/01S board works at 3.3V.

![image](https://github.com/user-attachments/assets/efd118e6-d34c-4e83-a5a3-f5a5e14d37ed)
https://www.google.com/url?sa=i&url=https%3A%2F%2Fwww.instructables.com%2FFTDI-ESP8266-Definitive-Wiring%2F&psig=AOvVaw3O8pTu-lbvlt2pClbHsHaq&ust=1749994602547000&source=images&cd=vfe&opi=89978449&ved=0CBcQjhxqFwoTCMiLhoqE8Y0DFQAAAAAdAAAAABAE

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
  delay(3000); // for 2 seconds
}
  </code>
</pre>

And here you can also see a short video. 👍

https://youtube.com/shorts/QKwVWmvhdyg?feature=share 

#JLCPCB #JLCONE
