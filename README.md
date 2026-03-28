
**Hello everyone!**

We continue with the ESP32 2.8 inch display development board from Elecrow.

It is very important to watch this video, it's very helpful, it will introduce you to LVGL library and Square Line Studio.

https://www.youtube.com/watch?v=LXoKEsqQGDk&list=PLwh4PlcPx2Gfrtm7TmlARyF4ccTmIy-gK&index=3&pp=iAQB

I built a DIY environment monitor using the ENS160. The circuit is very simple, the ENS160 communicates with the ESP board via the I2C protocol. 

With this module we have the capability to monitor:

• temperature (°C);

• relative humidity;

• air quality;

• estimated carbon dioxide (eCO2);

• total volatile organic compounds (TVOC);

I followed the Elecrow tutorial and I can say that I managed to create a starter project that I am making available to you. I am also attaching the project files from Square Line Studio, I think you will be able to import them and modify them yourself as you wish.

For start, it is a minimalist monitor that displays 3 measurements, as you can see below, but it can be improved for example by adding a graph to show the evolution of the measurements. Also, various signaling components can be introduced, such as an LED or a buzzer.

![Pic2](https://github.com/user-attachments/assets/9cd83acf-0975-4786-8de1-edf56fd4471a)

![Pic1](https://github.com/user-attachments/assets/9a3cbc7a-609c-4674-bc38-e6688231da17)


That's all for today!
