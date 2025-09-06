Hello makers!

Next, I created a small application using the ESP32-C6 mounted on the expansion board I created.

I also show you a small demonstration application, it's about displaying temperature and humidity using DHT22 and a 0.96" OLED display. The circuit is simple, DHT22 is connected to pin D7 and the display is on the I2C interface, so we are using SDA and SCL signals, and you can find the program below. Customize it as you wish. 🤓

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

I managed to build v2 of the sketch, there a few simple changes about how the temperature and humidity are displayed, as you can see below:

![20250906_125054 program v2](https://github.com/user-attachments/assets/4daedc31-da8a-4adc-8621-58e38bde65fa)

<pre>
  <code>
  /*
  DF Robot ESP32-C6
  DHT22
  OLED 0.91"  
  
  Display the values as:
  00.00 °C
  00.00 %R
*/

#include <Arduino.h>
#include <U8g2lib.h>  // Import font library
#include <Wire.h>
#include <DHT.h>

U8G2_SSD1306_128X64_NONAME_F_HW_I2C u8g2(U8G2_R0, U8X8_PIN_NONE);

#define DHTPIN 7         // Digital pin connected to the sensor
#define DHTTYPE DHT22    // DHT 22 (AM2302)

DHT dht(DHTPIN, DHTTYPE);

// Variables for non-blocking timing using millis()
unsigned long previousMillis = 0;
const unsigned long interval = 1000;  // Update every 1 second

void setup() {
  Serial.begin(115200);
  u8g2.begin();
  u8g2.setFontPosTop();  // Set text positioning to the top
  dht.begin();
}

void loop() {
  unsigned long currentMillis = millis();
  
  // Check if it's time to update the display
  if (currentMillis - previousMillis >= interval) {
    previousMillis = currentMillis;
    
    // Read sensor values
    float temp = dht.readTemperature();
    float humi = dht.readHumidity();
    
    // Format readings into strings as "00.00°C" and "00.00%R"
    // Insert the degree symbol explicitly as a single byte using '\xB0'
    char tempStr[16];
    char humiStr[16];
    sprintf(tempStr, "%05.2f% cC", temp, '\xB0'); // add the ° sign next to the temperature value
    sprintf(humiStr, "%05.2f% %R", humi); // add %R next to the humidity value
    
    // Update OLED display
    u8g2.clearBuffer();
    u8g2.setFont(u8g2_font_osb18_tf);   // Select a clear, large font
    u8g2.drawStr(0, 10, tempStr);         // Display temperature on the first line
    u8g2.drawStr(0, 40, humiStr);         // Display humidity on the second line
    u8g2.sendBuffer();
  }
}

  <code>
<pre>


If you want to see a few simple projects using this board then just go back to the main page.
