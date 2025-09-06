Hi makers!

We have another application with ESP32-C6, something common, but this time we use 8x32 MAX7219 matrix display panel. The connections are simple, just pay attention to the parts of the program where we defined the pins used for DHT22 and MAX7219.

![humidity display](https://github.com/user-attachments/assets/f20e16e6-fbf2-4ea9-b7e7-7003a951bf8f)

![temperature display](https://github.com/user-attachments/assets/589e6f5e-666b-40c4-b9fd-c25415051de9)


<pre>
  <code>
  // Source: https://wokwi.com/projects/289186888566178317

/* Display only temperature and humiditiy every 5 seconds
 * Use of ESP32-C6, MAX72XX, DTH22 components to 
 * print some information on the display.
 *
 * for more examples:
 * https://github.com/MajicDesigns/MD_Parola/tree/main/examples
 * https://github.com/MajicDesigns/MD_MAX72XX/tree/main/examples
 */

// Header file includes
#include <MD_Parola.h>
#include <MD_MAX72xx.h>
#include <DHT.h>
#include <SPI.h>
#include <Wire.h>
#include "Font7Seg.h" // if you wish to use it

// Define the number of devices we have in the chain and the hardware interface
// NOTE: These pin numbers will probably not work with your hardware and may
// need to be adapted
#define HARDWARE_TYPE MD_MAX72XX::FC16_HW
#define MAX_DEVICES 4  // Define the number of displays connected
#define CLK_PIN 23     // CLK or SCK
#define DATA_PIN 22    // DATA or MOSI
#define CS_PIN 21      // CS or SS
#define SPEED_TIME 75  // Speed of the transition
#define PAUSE_TIME 0
#define MAX_MESG 20

char szMesg[MAX_MESG + 1] = "";

// These are for the temperature
#define DHTPIN 7 // we are using this digital pin from ESP32-C6
#define DHTTYPE DHT22
#define TIMEDHT 5000 // switch between temp and humid every 5 seconds

float humidity, celsius;

uint8_t degC[] = { 3, 0, 3, 3 }; // create degree sign as 4 dots :: in the top right corner

uint32_t timerDHT = TIMEDHT;

DHT dht(DHTPIN, DHTTYPE);

// Hardware SPI connection
MD_Parola P = MD_Parola(HARDWARE_TYPE, CS_PIN, MAX_DEVICES);

// Code for get Temperature
void getTemperature() {
  // Wait for a time between measurements
  if ((millis() - timerDHT) > TIMEDHT) {
    // Update the timer
    timerDHT = millis();

    // Reading temperature or humidity takes about 250 milliseconds!
    // Sensor readings may also be up to 2 seconds 'old' (its a very slow sensor)
    humidity = dht.readHumidity();

    // Read temperature as Celsius (the default)
    celsius = dht.readTemperature();

    // Check if any reads failed and exit early (to try again)
    if (isnan(humidity) || isnan(celsius)) {
      Serial.println("Failed to read from DHT sensor!");
      return;
    }
  }
}


void setup(void) {

  Wire.begin();

  P.begin(2);
  P.setInvert(false);
  //P.setIntensity(1);
  P.setZone(0, MAX_DEVICES - 4, MAX_DEVICES - 1);
  P.setZone(1, MAX_DEVICES - 4, MAX_DEVICES - 1);

  P.displayZoneText(0, szMesg, PA_CENTER, SPEED_TIME, 0, PA_PRINT, PA_NO_EFFECT);

  P.addChar('$', degC); // create a pseudo for the degree sign

  dht.begin();
}

void loop(void) {
  static uint32_t lastTime = 0;  // Memory (ms)
  static uint8_t display = 0;    // Current display mode

  getTemperature();

  P.displayAnimate();

  if (P.getZoneStatus(0)) {
    switch (display) {
      case 0:  // Temperature deg Celsius
        P.setPause(0, 10000);
        P.setTextEffect(0, PA_SCROLL_LEFT, PA_SCROLL_UP);
        display++;
        dtostrf(celsius, 3, 1, szMesg);
        strcat(szMesg, "$C");
        break;

      case 1:  // Humidity
        P.setTextEffect(0, PA_SCROLL_DOWN, PA_SCROLL_LEFT);
        display = 0;  // go back to the temperature
        dtostrf(humidity, 3, 1, szMesg);
        strcat(szMesg, "%R");
        break;
    }

    P.displayReset(0);  // Reset display zone
  }

}  // loop
   
  </code>
</pre>

