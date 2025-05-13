This is the board from DFRobot called Beetle ESP32-C6, a real coin size board:


![94a6cfae52fad3dc8896f1760ea6adb8](https://github.com/user-attachments/assets/d1e970e9-4984-4ea9-bf9d-64b3e5a6374a)


![51ab86bba659126748111cb59bb4b12a](https://github.com/user-attachments/assets/f0609c4e-dc5f-4207-afd3-54aaf112a125)


![20250406_125345](https://github.com/user-attachments/assets/6092a755-6e5b-4aeb-83d6-145e701ca79e)


![20250406_125355](https://github.com/user-attachments/assets/d2e450b3-999a-45ce-b3a3-ecac13aa1f37)

More details can be found by accessing the links 😁:

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

I also show you a small demonstration application, it's about displaying temperature and humidity using DHT22 and a 0.96" OLED display. The circuit is simple, DHT22 is connected to pin D7 and the display is on the I2C interface, so SDA and SCL, and you can find the program below. Customize it as you wish. 🤓

![20250513_184421](https://github.com/user-attachments/assets/d747b125-022e-4b65-bef4-bf65bd3acc0f)

<pre>
  <code>
/*
  DF Robot ESP32-C6
  DHT22
  OLED 0.91"  
  
  Display data as:
  Temp: 00.00
  Humi: 00.00
*/
#include <Arduino.h>
#include <U8g2lib.h>  //Import font library
//#include <SPI.h>
#include <Wire.h>

#include <DHT.h>

U8G2_SSD1306_128X64_NONAME_F_HW_I2C u8g2(/* rotation=*/U8G2_R0, /* reset=*/U8X8_PIN_NONE);

#define DHTPIN 7   // What digital pin we're connected to

// Uncomment whatever type you're using!
//#define DHTTYPE DHT11     // DHT 11
#define DHTTYPE DHT22  // DHT 22, AM2302, AM2321
//#define DHTTYPE DHT21   // DHT 21, AM2301

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(115200);
  u8g2.begin();
  u8g2.setFontPosTop();  //When you use drawStr to display strings, the default criteria is to display the lower-left coordinates of the characters. The function can be understood as changing the coordinate position to the upper left corner of the display string as the coordinate standard.
  //Initialize the sensor
  dht.begin();
}

void loop() {
  //Clear display
  u8g2.clearBuffer();
  //Assign reading to temp and humi for displaying
  float humi = dht.readHumidity();
  // Read temperature as Celsius (the default)
  float temp = dht.readTemperature();
  //Display temperature
  u8g2.setFont(u8g2_font_osb18_tf);  // Select font type and size(see official)
  u8g2.drawStr(5, 10, "Temp");       //Write character to the specified position
  u8g2.setFont(u8g2_font_t0_18b_tr);
  u8g2.setCursor(75, 15);  //Display content from this position
  u8g2.print(temp);
  //Display humidity
  u8g2.setFont(u8g2_font_osb18_tf);
  u8g2.drawStr(5, 40, "Humi");
  u8g2.setFont(u8g2_font_t0_18b_tr);
  u8g2.setCursor(75, 45);
  u8g2.print(humi);
  u8g2.sendBuffer();
  delay(1000);
}
  </code>
</pre>




