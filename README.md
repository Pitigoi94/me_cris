Hello everyone!

I made a small, slightly interactive application, I might add, "which with a gesture can change the fate of the galaxy". 😁
The application is inspired by the Star Wars theme. I noticed in an online video from another maker how he used a buzzer in order to reproduce the imperial soundtrack from Star Wars movie, and another application with the classic opening sound. Thanks to the author for sharing them [https://github.com/robsoncouto/arduino-songs  ]. In addition to these, I added a panel with LED matrices, since we also have control, through the "power of the force". Although I would have liked to use 2 IR sensors, but I don't have them, so for example I use push buttons.
List of components:
• 1x 8x32 MAX7219 matrix panel;
• 1x XIAO ESPre-C3;
• 3x buzzers;
• 3x push buttons;
• 3x 10kΩ resistors;
• 5V power suuply;
• breadboard, wires and so on.
Below you have a circuit diagram and also a block diagram [check your available components]:

<img width="936" height="650" alt="image" src="https://github.com/user-attachments/assets/80f2979c-2139-4de5-9bc1-4b94141c98cf" />

<img width="342" height="342" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/1046a7b0-4dbc-4a58-be48-a26c444c8f57" />

• INPUTS:
→ 2 push buttons, #1 and #2;
→ 1 push button (#3), as a reset.
• OUTPUTS:
→ 3 buzzers, #1 and #2 are for the imperial soundtrack, and #3 for the beginning one;
→ 1 matrix panel on which various messages can be displayed.
• CORE:
→ in the middle of the application we have a Xiao ESP32-C3.

The program seems a bit long, but it is not that difficult, as a pseudo code can be described like this:
• in the "MSG_IDLE" state:
→ the matrix panel displays the message "May the Force be with you!";
→ the buzzers are off;
→ a command is expected through one of the two push buttons;
• the "MSG_RED" state is triggered when:
→ I press button #1;
→ the matrix panel displays the message "I am your father!";
→ buzzer #3 will play the imperial soundtrack;
→ after the song ends, the buzzer stops and automatically returns to the "IDLE" state;
• the "MSG_GREEN" state is triggered when:
→ I press button #2;
→ the matrix panel displays the message "XIAO from ESP32-C3 I am!";
→ buzzers #1 and #2 will play the opening soundtrack;
→ after the song ends, the buzzers stop and it automatically returns to the "MSG_IDLE" state.
The push button acts as a RESET, whenever it is pressed the program is forced to return to the MSG_IDLE state.
In fact, you can force the MSG_RED state to MSG_GREEN and vice versa at any time by pressing button #1 or #2.

<pre>
<code>
// Some libraries
#include <MD_Parola.h>
#include <MD_MAX72xx.h>
#include <SPI.h>

// Connections
#define HARDWARE_TYPE MD_MAX72XX::FC16_HW
#define MAX_DEVICES 4
#define CLK_PIN D8   // SCK
#define DATA_PIN D10  // MOSI
#define CS_PIN D9    // SS
MD_Parola matrix = MD_Parola(HARDWARE_TYPE, CS_PIN, MAX_DEVICES);

// Scrolling messages
const char* MSG_ONE = "I am your father!"; // message 1
const char* MSG_TWO = "XIAO from ESP32-C3 I am!"; // message 2
const char* MSG_IDLE = "May the Force be with you!"; // initial message
enum MsgState { Mode_Idle,
                Mode_One,
                Mod_Two };
MsgState currMsg = Mode_Idle;

// Buttons pins
const int BTN_RED_PIN = D4;    // plays first melody
const int BTN_GREEN_PIN = D5;  // plays second melody
const int BTN_RESET_PIN = D6;  // resets to idle

// Buzzer outputs
const int RED_BUZZER_PIN = D0;
const int GREEN_BUZZER1_PIN = D1;
const int GREEN_BUZZER2_PIN = D2;

// State machine 
enum { ST_IDLE,
       ST_RED_PLAY,
       ST_GREEN_PLAY } state = ST_IDLE;

// Previous buttons states
bool prevBtnRed = HIGH;
bool prevBtnGreen = HIGH;

// Buzzer notes
#define NOTE_B0 31
#define NOTE_C1 33
#define NOTE_CS1 35
#define NOTE_D1 37
#define NOTE_DS1 39
#define NOTE_E1 41
#define NOTE_F1 44
#define NOTE_FS1 46
#define NOTE_G1 49
#define NOTE_GS1 52
#define NOTE_A1 55
#define NOTE_AS1 58
#define NOTE_B1 62
#define NOTE_C2 65
#define NOTE_CS2 69
#define NOTE_D2 73
#define NOTE_DS2 78
#define NOTE_E2 82
#define NOTE_F2 87
#define NOTE_FS2 93
#define NOTE_G2 98
#define NOTE_GS2 104
#define NOTE_A2 110
#define NOTE_AS2 117
#define NOTE_B2 123
#define NOTE_C3 131
#define NOTE_CS3 139
#define NOTE_D3 147
#define NOTE_DS3 156
#define NOTE_E3 165
#define NOTE_F3 175
#define NOTE_FS3 185
#define NOTE_G3 196
#define NOTE_GS3 208
#define NOTE_A3 220
#define NOTE_AS3 233
#define NOTE_B3 247
#define NOTE_C4 262
#define NOTE_CS4 277
#define NOTE_D4 294
#define NOTE_DS4 311
#define NOTE_E4 330
#define NOTE_F4 349  
#define NOTE_FS4 370
#define NOTE_G4 392
#define NOTE_GS4 415  
#define NOTE_A4 440
#define NOTE_AS4 466
#define NOTE_B4 494
#define NOTE_C5 523
#define NOTE_CS5 554
#define NOTE_D5 587
#define NOTE_DS5 622
#define NOTE_E5 659
#define NOTE_F5 698
#define NOTE_FS5 740
#define NOTE_G5 784
#define NOTE_GS5 831
#define NOTE_A5 880
#define NOTE_AS5 932
#define NOTE_B5 988
#define NOTE_C6 1047
#define NOTE_CS6 1109
#define NOTE_D6 1175
#define NOTE_DS6 1245
#define NOTE_E6 1319
#define NOTE_F6 1397
#define NOTE_FS6 1480
#define NOTE_G6 1568
#define NOTE_GS6 1661
#define NOTE_A6 1760
#define NOTE_AS6 1865
#define NOTE_B6 1976
#define NOTE_C7 2093
#define NOTE_CS7 2217
#define NOTE_D7 2349
#define NOTE_DS7 2489
#define NOTE_E7 2637
#define NOTE_F7 2794
#define NOTE_FS7 2960
#define NOTE_G7 3136
#define NOTE_GS7 3322
#define NOTE_A7 3520
#define NOTE_AS7 3729
#define NOTE_B7 3951
#define NOTE_C8 4186
#define NOTE_CS8 4435
#define NOTE_D8 4699
#define NOTE_DS8 4978

#define REST 0

// The Imperial March backsound
const int redTempo = 120;
const int redMelody[] = {
  NOTE_A4,-4, NOTE_A4,-4, NOTE_A4,16, NOTE_A4,16, NOTE_A4,16, NOTE_A4,16, NOTE_F4,8, REST,8,
  NOTE_A4,-4, NOTE_A4,-4, NOTE_A4,16, NOTE_A4,16, NOTE_A4,16, NOTE_A4,16, NOTE_F4,8, REST,8,
  NOTE_A4,4, NOTE_A4,4, NOTE_A4,4, NOTE_F4,-8, NOTE_C5,16,

  NOTE_A4,4, NOTE_F4,-8, NOTE_C5,16, NOTE_A4,2,//4
  NOTE_E5,4, NOTE_E5,4, NOTE_E5,4, NOTE_F5,-8, NOTE_C5,16,
  NOTE_A4,4, NOTE_F4,-8, NOTE_C5,16, NOTE_A4,2,
  
  NOTE_A5,4, NOTE_A4,-8, NOTE_A4,16, NOTE_A5,4, NOTE_GS5,-8, NOTE_G5,16, //7 
  NOTE_DS5,16, NOTE_D5,16, NOTE_DS5,8, REST,8, NOTE_A4,8, NOTE_DS5,4, NOTE_D5,-8, NOTE_CS5,16,

  NOTE_C5,16, NOTE_B4,16, NOTE_C5,16, REST,8, NOTE_F4,8, NOTE_GS4,4, NOTE_F4,-8, NOTE_A4,-16,//9
  NOTE_C5,4, NOTE_A4,-8, NOTE_C5,16, NOTE_E5,2,

  NOTE_A5,4, NOTE_A4,-8, NOTE_A4,16, NOTE_A5,4, NOTE_GS5,-8, NOTE_G5,16, //7 
  NOTE_DS5,16, NOTE_D5,16, NOTE_DS5,8, REST,8, NOTE_A4,8, NOTE_DS5,4, NOTE_D5,-8, NOTE_CS5,16,

  NOTE_C5,16, NOTE_B4,16, NOTE_C5,16, REST,8, NOTE_F4,8, NOTE_GS4,4, NOTE_F4,-8, NOTE_A4,-16,//9
  NOTE_A4,4, NOTE_F4,-8, NOTE_C5,16, NOTE_A4,2,
};
int redNotes = sizeof(redMelody) / sizeof(redMelody[0]) / 2;

// The Star Wars backsound
const int greenTempo = 108;
const int greenMelody[] = {
  NOTE_AS4, 8, NOTE_AS4, 8, NOTE_AS4, 8,  //1
  NOTE_F5, 2, NOTE_C6, 2,
  NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F6, 2, NOTE_C6, 4,
  NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F6, 2, NOTE_C6, 4,
  NOTE_AS5, 8, NOTE_A5, 8, NOTE_AS5, 8, NOTE_G5, 2, NOTE_C5, 8, NOTE_C5, 8, NOTE_C5, 8,
  NOTE_F5, 2, NOTE_C6, 2,
  NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F6, 2, NOTE_C6, 4,

  NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F6, 2, NOTE_C6, 4,  //8
  NOTE_AS5, 8, NOTE_A5, 8, NOTE_AS5, 8, NOTE_G5, 2, NOTE_C5, -8, NOTE_C5, 16,
  NOTE_D5, -4, NOTE_D5, 8, NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F5, 8,
  NOTE_F5, 8, NOTE_G5, 8, NOTE_A5, 8, NOTE_G5, 4, NOTE_D5, 8, NOTE_E5, 4, NOTE_C5, -8, NOTE_C5, 16,
  NOTE_D5, -4, NOTE_D5, 8, NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F5, 8,

  NOTE_C6, -8, NOTE_G5, 16, NOTE_G5, 2, REST, 8, NOTE_C5, 8,  //13
  NOTE_D5, -4, NOTE_D5, 8, NOTE_AS5, 8, NOTE_A5, 8, NOTE_G5, 8, NOTE_F5, 8,
  NOTE_F5, 8, NOTE_G5, 8, NOTE_A5, 8, NOTE_G5, 4, NOTE_D5, 8, NOTE_E5, 4, NOTE_C6, -8, NOTE_C6, 16,
  NOTE_F6, 4, NOTE_DS6, 8, NOTE_CS6, 4, NOTE_C6, 8, NOTE_AS5, 4, NOTE_GS5, 8, NOTE_G5, 4, NOTE_F5, 8,
  NOTE_C6, 1
};
int greenNotes = sizeof(greenMelody) / sizeof(greenMelody[0]) / 2;

// Playback trackers
bool redPlaying = false;
unsigned long redWholenote, redNoteStart;
int redIdx = 0;
int redNoteDur = 0;

bool greenPlaying = false;
unsigned long greenWholenote, greenNoteStart;
int greenIdx = 0;
int greenNoteDur = 0;

void setup() {
  // buttons
  pinMode(BTN_RED_PIN, INPUT);
  pinMode(BTN_GREEN_PIN, INPUT);
  pinMode(BTN_RESET_PIN, INPUT);

  // buzzers
  pinMode(RED_BUZZER_PIN, OUTPUT);
  pinMode(GREEN_BUZZER1_PIN, OUTPUT);
  pinMode(GREEN_BUZZER2_PIN, OUTPUT);

  // matrix init
  matrix.begin();
  matrix.setIntensity(5);
  matrix.displayClear();
  // show initial message
  matrix.displayText(
    MSG_IDLE, PA_CENTER, 50, 0,
    PA_SCROLL_LEFT, PA_SCROLL_LEFT);

  delay(100);  // let buttons settle
  prevBtnRed = digitalRead(BTN_RED_PIN);
  prevBtnGreen = digitalRead(BTN_GREEN_PIN);
} // void setup

void loop() {
  // Reset button state
  if (digitalRead(BTN_RESET_PIN) == LOW) {
    emergencyReset();
    return;
  }

  // Buttons #1 & #2 states 
  bool curBtnRed = digitalRead(BTN_RED_PIN);
  bool curBtnGreen = digitalRead(BTN_GREEN_PIN);
  bool pressBtnRed = (curBtnRed == LOW && prevBtnRed == HIGH);
  bool pressBtnGreen = (curBtnGreen == LOW && prevBtnGreen == HIGH);

  // Update state
  if (state == ST_RED_PLAY) setMessage(Mode_One);
  else if (state == ST_GREEN_PLAY) setMessage(Mod_Two);
  else setMessage(Mode_Idle);

  if (matrix.displayAnimate()) {
    matrix.displayReset();
  }

  // States machine
  switch (state) {
    case ST_IDLE:
      if (pressBtnRed) {
        beginRedMelody();
        state = ST_RED_PLAY;
      } else if (pressBtnGreen) {
        beginGreenMelody();
        state = ST_GREEN_PLAY;
      }
      break;

    case ST_RED_PLAY:
      updateRedMelody();
      if (!redPlaying) state = ST_IDLE;
      else if (pressBtnGreen) {
        // mid-tune override
        redPlaying = false;
        noTone(RED_BUZZER_PIN);
        beginGreenMelody();
        state = ST_GREEN_PLAY;
      }
      break;

    case ST_GREEN_PLAY:
      updateGreenMelody();
      if (!greenPlaying) state = ST_IDLE;
      else if (pressBtnRed) {
        greenPlaying = false;
        noTone(GREEN_BUZZER1_PIN);
        noTone(GREEN_BUZZER2_PIN);
        beginRedMelody();
        state = ST_RED_PLAY;
      }
      break;
  }

  // Update the previous button states
  prevBtnRed = curBtnRed;
  prevBtnGreen = curBtnGreen;
}


void setMessage(MsgState want) {
  if (want == currMsg) return;
  currMsg = want;
  const char* txt =
    (want == Mode_One) ? MSG_ONE : (want == Mod_Two) ? MSG_TWO
                                                  : MSG_IDLE;
  matrix.displayClear();
  matrix.displayReset();
  matrix.displayText(txt,
                     PA_LEFT, 50, 0,
                     PA_SCROLL_LEFT, PA_SCROLL_LEFT);
}

// — Stop everything & go idle again —
void emergencyReset() {
  redPlaying = greenPlaying = false;
  noTone(RED_BUZZER_PIN);
  noTone(GREEN_BUZZER1_PIN);
  noTone(GREEN_BUZZER2_PIN);
  state = ST_IDLE;
  setMessage(Mode_Idle);
}

// — Start RED melody from the top —
void beginRedMelody() {
  redWholenote = (60000L * 4) / redTempo;
  redIdx = 0;
  redPlaying = true;
  redNoteStart = millis() - 1;
}

// — Non-blocking step through RED melody —
void updateRedMelody() {
  if (!redPlaying) return;
  unsigned long now = millis();
  if (now - redNoteStart >= redNoteDur) {
    noTone(RED_BUZZER_PIN);
    if (redIdx >= redNotes * 2) {
      redPlaying = false;
      return;
    }
    int divider = redMelody[redIdx + 1];
    redNoteDur = (divider > 0)
                   ? redWholenote / divider
                   : (redWholenote / abs(divider)) * 1.5;
    tone(RED_BUZZER_PIN,
         redMelody[redIdx],
         redNoteDur * 0.9);
    redNoteStart = now;
    redIdx += 2;
  }
}

// — Start GREEN melody from the top —
void beginGreenMelody() {
  greenWholenote = (60000L * 4) / greenTempo;
  greenIdx = 0;
  greenPlaying = true;
  greenNoteStart = millis() - 1;
}

// — Non-blocking step through GREEN melody —
void updateGreenMelody() {
  if (!greenPlaying) return;
  unsigned long now = millis();
  if (now - greenNoteStart >= greenNoteDur) {
    noTone(GREEN_BUZZER1_PIN);
    noTone(GREEN_BUZZER2_PIN);
    if (greenIdx >= greenNotes * 2) {
      greenPlaying = false;
      return;
    }
    int divider = greenMelody[greenIdx + 1];
    greenNoteDur = (divider > 0)
                     ? greenWholenote / divider
                     : (greenWholenote / abs(divider)) * 1.5;
    tone(GREEN_BUZZER1_PIN,
         greenMelody[greenIdx],
         greenNoteDur * 0.9);
    tone(GREEN_BUZZER2_PIN,
         greenMelody[greenIdx],
         greenNoteDur * 0.9);
    greenNoteStart = now;
    greenIdx += 2;
  }
}
</code>
</pre>

![image](https://github.com/user-attachments/assets/b7bd91c4-19bb-4f37-a01a-04ce03877cd5)


What do you think? Have fun with! 🙂

*** Content created also using AI.


