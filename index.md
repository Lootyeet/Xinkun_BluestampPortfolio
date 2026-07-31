**RFID Lockbox**

A normal safe uses a combination lock; the RFID Lockbox uses an RFID tag sensor and tag instead to control the lock. The project you will see below uses this mechanism to unlock and lock the safe through a solenoid, which, in simple terms, is a magnet that can be turned off and on; the RFID tag is inserted into a slot where it is read by the RFID tag sensor, and if it isn't the correct tag, then it will be kept in the safe. If the correct tag is inserted and read, then it will turn the solenoid off and thus allow the user to open the safe to retrieve or place their valuables inside. 

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Xinkun L. | Canyon Crest Academy | Electrical Engineering | Incoming Junior

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/qeqdiUDOUYE?si=rNsEbZMbVaFBKRgt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My goal for the second milestone was finishing the base project/combining the circuit with the physical lockbox. I was able to make the lockbox, fit all the wiring inside it, and get it working, while also making preparations for my future modifications. During the completion of this, I had to face damaged batteries from miswiring, modifying my lock due to it not working as intended, and many other issues. But through working through them, I was able to improve my ability to use my materials in unique ways to solve problems, and was able to learn how to debug my wiring and test it to make sure it works. During the time of creating the circuit, the lockbox, and combining them, what surprised me the most was how much the finished product ended up being compared to what I had thought of in the beginning. Despite it looking somewhat similar to what I had in mind, the many changes I had to make to get certain parts to work as I had hoped led to many modifications to what I had originally planned. As to the completion of my final milestone for this project, I need to finish the modification to it that I had laid out during the completion of this milestone and potentially add more to it. 

# First Milestone: Finish Building The Circuit And RFID Tag Reader

<iframe width="560" height="315" src="https://www.youtube.com/embed/ur9CDYwbdSo?si=tKRHFVfpNjszn-9u" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


During the first milestone of this project, I used female-to-male wires, jumper wires, resistors, an RFID reader, LEDs, an Arduino board, a solenoid, and the Arduino IDE to code the circuit's functionality. The wires I used to connect the circuit and the RFID sensor alongside the LEDs and the solenoid so that, through the code, the right RFID tag will activate and deactivate the solenoid, which will later allow the lockbox to open and lock. The LEDs show if the tag is the correct one or not through the use of the red LED indicating a wrong RFID tag getting scanned and a green LED indicating the right RFID tag getting scanned. They will eventually fit into the case of the actual lockbox, which I will make out of cardboard to start with. Due to my little experience with Arduino as a whole and most of the items, such as the RFID sensor and the solenoid, I have had to search up what they do, guides on how to wire them, and guides on how to actually upload the code and how to make the code in the first place. For the code I currently have in my Arduino, it is something I used from another creator and modified to work with my solenoid. Most of my challenges came from the inexperience of using such materials, but I was able to overcome that through research and testing as well as asking for help on some parts. Thus, through overcoming those challenges, I was able to learn how to use the many different electronic parts and how to code using Arduino IDE. I plan to integrate the circuit I have made so far into the lockbox I will make in the future and make modifications from there, including changes to code or physical changes. One of these includes making the card reader a sort of slot where, if you have the incorrect RFID tag, it will keep the card inside the safe through a motor dropping it, and if it is the correct RFID tag, then it will allow the user to take it back out.
# Schematics 

![TinkerCAD Circuit](docs/assets/css/Circuit.png)

# Code

```cpp
#include <SPI.h> 
#include <RFID.h>
#include <Servo.h> 
#include <Keypad.h>

// --- RFID SETUP ---
RFID rfid(10, 9);      
unsigned char status; 
unsigned char str[MAX_LEN]; 
String accessGranted[1] = {"336871537"};  
int accessGrantedSize = 1;                                

// --- KEYPAD SETUP ---
const byte ROWS = 4; 
const byte COLS = 4; 
char keys[ROWS][COLS] = {
  {'1','2','3','A'},
  {'4','5','6','B'},
  {'7','8','9','C'},
  {'*','0','#','D'}
};
byte rowPins[ROWS] = {2, 4, 7, A0}; 
byte colPins[COLS] = {A1, A2, A3, A4}; 
Keypad keypad = Keypad(makeKeymap(keys), rowPins, colPins, ROWS, COLS);

const int pinLength = 4;
char secretPIN[pinLength] = {'1', '2', '3', '4'}; 
char enteredPIN[pinLength];
int currentPosition = 0;

// --- STATE MACHINE & SECURITY TRACKING ---
enum SystemState { WAITING_FOR_CARD, WAITING_FOR_PIN, SYSTEM_LOCKED };
SystemState currentState = WAITING_FOR_CARD;

int failedAttempts = 0;        
unsigned long stateTimer = 0;  

// Variables for the non-blocking green LED flash
unsigned long flashTimer = 0;
boolean greenLedState = LOW;

// --- HARDWARE SETUP ---
Servo lockServo;                
int lockPos = 75;               // Servo position to DROP the card
int unlockPos = 165;            // Servo position to HOLD the card
boolean locked = true;

int redLEDPin = 5;
int greenLEDPin = 6;
int solenoidPin = 8; 

void setup() 
{ 
  Serial.begin(9600);     
  SPI.begin();            
  rfid.init();            
  
  pinMode(redLEDPin, OUTPUT);     
  pinMode(greenLEDPin, OUTPUT);
  pinMode(solenoidPin, OUTPUT); 

  // Startup LED sequence
  digitalWrite(redLEDPin, HIGH);
  delay(200);
  digitalWrite(greenLEDPin, HIGH);
  delay(200);
  digitalWrite(redLEDPin, LOW);
  delay(200);
  digitalWrite(greenLEDPin, LOW);
  
  // Initialize trapdoor servo to the holding position
  lockServo.attach(3);
  lockServo.write(unlockPos);        
  
  Serial.println("System Ready. Place card/tag in slot...");
} 

void loop() 
{ 
  switch (currentState) {
    
    // ==========================================
    // STATE 1: WAITING FOR RFID CARD
    // ==========================================
    case WAITING_FOR_CARD: {
      String scannedCard = checkRFID();
      if (scannedCard != "") {
        Serial.println("Card ID : " + scannedCard);
        
        if (isCardAuthorized(scannedCard)) {
          Serial.println("Valid Card! You have 10 seconds to enter PIN...");
          currentState = WAITING_FOR_PIN;
          currentPosition = 0;
          stateTimer = millis(); 
          flashTimer = millis(); // Initialize the flashing timer
        } else {
          // Card is unauthorized. Trigger denied sequence AND drop the card!
          executeAccessDenied(true); 
        }
      }
      break;
    }

    // ==========================================
    // STATE 2: WAITING FOR KEYPAD PIN
    // ==========================================
    case WAITING_FOR_PIN: {
      // Non-blocking Green LED Flashing (Toggles every 250 milliseconds)
      if (millis() - flashTimer >= 250) {
        flashTimer = millis();
        greenLedState = !greenLedState; 
        digitalWrite(greenLEDPin, greenLedState);
      }

      // Check 10-Second Timeout
      if (millis() - stateTimer > 10000) {
        Serial.println("Timeout! Took too long to enter PIN.");
        // False = Do not actuate servo, just flash red LEDs
        executeAccessDenied(false);
        failedAttempts++;
        
        if (failedAttempts >= 3) {
          enterLockout();
        } else {
          resetToCardWait();
        }
      }

      char key = keypad.getKey();
      if (key) { 
        enteredPIN[currentPosition] = key;
        currentPosition++; 
        Serial.print("*"); 

        // If they entered 4 digits, check the PIN
        if (currentPosition == pinLength) {
          Serial.println(); 
          
          if (checkPINMatch()) {
            executeAccessGranted();
            failedAttempts = 0; 
            resetToCardWait();
          } else {
            // Wrong PIN entered. Flash red LEDs, but DO NOT actuate the servo
            executeAccessDenied(false);
            failedAttempts++;
            
            if (failedAttempts >= 3) {
              enterLockout();
            } else {
              Serial.println("Try again. You have 10 seconds.");
              currentPosition = 0;
              stateTimer = millis(); 
            }
          }
        }
      }
      break;
    }

    // ==========================================
    // STATE 3: SYSTEM LOCKED OUT
    // ==========================================
    case SYSTEM_LOCKED: {
      // Check 1-Minute Timeout (60,000 milliseconds)
      if (millis() - stateTimer >= 60000) {
        Serial.println("Lockout period ended.");
        exitLockout();
      } else {
        // Allow an authorized RFID card to override the lockout
        String scannedCard = checkRFID();
        if (scannedCard != "") {
          if (isCardAuthorized(scannedCard)) {
            Serial.println("Override Authorized! Lockout bypassed.");
            digitalWrite(redLEDPin, LOW); 
            
            // Go straight to PIN entry mode
            currentState = WAITING_FOR_PIN;
            currentPosition = 0;
            stateTimer = millis();
            flashTimer = millis();
            failedAttempts = 0;
          } else {
            // Someone tried to bypass the lockout with a fake card. Confiscate it!
            Serial.println("Invalid override card! Confiscating...");
            lockServo.write(lockPos); // Open trapdoor
            delay(800);               // Wait for it to fall
            lockServo.write(unlockPos); // Close trapdoor
          }
        }
      }
      break;
    }
  }
}

// --- HELPER FUNCTIONS ---

String checkRFID() {
  String temp = "";
  if (rfid.findCard(PICC_REQIDL, str) == MI_OK) { 
    if (rfid.anticoll(str) == MI_OK) { 
      for (int i = 0; i < 4; i++) { 
        temp = temp + (0x0F & (str[i] >> 4)); 
        temp = temp + (0x0F & str[i]); 
      } 
    } 
    rfid.selectTag(str); 
  }
  rfid.halt();
  return temp;
}

boolean isCardAuthorized(String temp) {
  for (int i=0; i < accessGrantedSize; i++) {
    if(accessGranted[i] == temp) return true;
  }
  return false;
}

boolean checkPINMatch() {
  for (int i = 0; i < pinLength; i++) {
    if (enteredPIN[i] != secretPIN[i]) return false; 
  }
  return true; 
}

void executeAccessGranted() {
  Serial.println("Access Granted - 2FA Successful");
  
  // Turn green LED solid to indicate success
  digitalWrite(greenLEDPin, HIGH); 
  
  if (locked == true) {
      digitalWrite(solenoidPin, HIGH);
      locked = false;
  } else {
      digitalWrite(solenoidPin, LOW);
      locked = true;
  }
  
  // Hold the solid green LED on for 2 seconds so the user can see it
  delay(2000); 
}

void executeAccessDenied(boolean dropCard) {
  // Immediately turn off the flashing green LED
  digitalWrite(greenLEDPin, LOW); 
  
  Serial.println("Access Denied");

  if (dropCard) {
    Serial.println("Dropping unauthorized card into lockbox...");
    lockServo.write(lockPos); // Open the trapdoor
  }
  
  // Red LED angry blinks (Takes about 800ms)
  for(int i=0; i<2; i++){
    digitalWrite(redLEDPin, HIGH); delay(200);
    digitalWrite(redLEDPin, LOW); delay(200);
  }

  if (dropCard) {
    lockServo.write(unlockPos); // Close the trapdoor
    delay(200);
  }
}

void enterLockout() {
  // Ensure green LED is off during lockout
  digitalWrite(greenLEDPin, LOW); 
  
  Serial.println("MAX ATTEMPTS REACHED. SYSTEM LOCKED FOR 1 MINUTE.");
  currentState = SYSTEM_LOCKED;
  stateTimer = millis(); 
  digitalWrite(redLEDPin, HIGH); 
}

void exitLockout() {
  failedAttempts = 0; 
  digitalWrite(redLEDPin, LOW); 
  resetToCardWait();
}

void resetToCardWait() {
  // Ensure the green LED is off when returning to standby mode
  digitalWrite(greenLEDPin, LOW); 
  
  currentState = WAITING_FOR_CARD;
  currentPosition = 0;
  Serial.println("-----------------------------------");
  Serial.println("System Ready. Place card/tag in slot...");
}
```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Solenoid | Used For Locking Mechanism | $9.99 | <a href="https://www.amazon.com/KEYESTUDIO-Electromagnet-Module-Arduino-Environmental-Friendly/dp/B07H3V8N2Q/"> Link </a> |
| RFID Kit | Used As The Opening And Closing Activation Mechanism | $9.99 | <a href="https://www.amazon.com/HiLetgo-3pcs-RFID-Kit-Raspberry/dp/B07VLDSYRW/"> Link </a> |
| Magnets | Used For Mechanisms In The Lockbox | $3.99 | <a href="https://www.amazon.com/Towjug-Adhesive-3M-Anisotropy-whiteboards/dp/B0CQLHFSGF/"> Link </a> |
| Cardboard | Used To Make The Physical Lockbox | $7.99 | <a href="https://www.amazon.com/Corrugated-Cardboard-Inserts-Shipping-Mailing/dp/B0GSJ7K4G7/"> Link </a> |
| Digital Multimeter | Debugging The Circuit | $9.98 | <a href="https://www.amazon.com/Multimeter-Voltmeter-Continuity-Resistance-Electrical/dp/B0CXM242J1/"> Link </a> |
| Uno R3 Project | Used To Create The Circuit | $59.99 | <a href="https://www.amazon.com/EL-KIT-001-Project-Complete-Starter-Tutorial/dp/B01CZTLHGE/"> Link </a> |
| Tape | Used To Keep Everything Together | $4.48 | <a href="https://www.amazon.com/Scotch-3105-Magic-Tape-Pack/dp/B071VP1PC6/"> Link </a> |
| Batteries | Used To Power The Circuit | $5.99 | <a href="https://www.amazon.com/PKCELL-9V-Batteries-Battery-Detector/dp/B09MFQPQFY/"> Link </a> |
| Power Jack | Used To Connect The Extra Battery To The Solenoid | $3.97 | <a href="https://www.amazon.com/Battery-Connector-Electronics-Experiment-Research/dp/B0D9VT2FMF/"> Link </a> |
| Screwdriver Kit | Used For The Step Down Chip | $5.69 | <a href="https://www.amazon.com/Screwdriver-Different-Flathead-Screwdrivers-Precision/dp/B08ZS76VDG?th=1"> Link </a> |
| Step Down Chip | Used To Lower The Voltage Of The 9V Battery To 5V That Is Connected To The Solenoid | $6.99 | <a href="https://www.amazon.com/Seloky-Converter-Regulator-Adjustable-Voltmeter/dp/B0DM946DHG/"> Link </a> |
| Wire Strippers | Used To Strip The Power Jack Wires | $7.19 | <a href="https://www.amazon.com/ANGELSWORD-Stripper-Crimping-Crimper-Multi-Function/dp/B0DYP7CFZZ/"> Link </a> |
| Safety Goggles | Used For Safety When Stripping The Wires | $12.99 | <a href="https://www.amazon.com/SUPERMORE-Protective-Wide-Vision-Adjustable-Lightweight/dp/B07VF3C2CW/"> Link </a> |
| Scissors | Used To Cut The Cardboard And Tape | $9.97 | <a href="https://www.amazon.com/Westcott-13901-Straight-Titanium-Scissors/dp/B000P0LNRE/"> Link </a> |
| 4 AA Battery Holder | Used To Hold The 4 AA Batteries That Power The Solenoid And Servo Motor | $5.98 | <a href="https://www.amazon.com/LAMPVPATH-Battery-Holder-Leads-Wires/dp/B07T7MTRZX"> Link </a> |
| 4 AA Batteries | Used To Power The Solenoid And Servo Motor | $5.07 | <a href="https://www.amazon.com/Duracell-CopperTop-Batteries-All-Purpose-Household/dp/B00000JHQ6"> Link </a> |
| Compact Splicing Connector Assortment| Used To Connect The Battery Pack To The Solenoid And Servo Motor | $12.45 | <a href="https://www.amazon.com/Compact-Splicing-Connector-Assortment-221-2401/dp/B0CJ5QF4Z2"> Link </a> |

# Resources
- [Video Guide](https://www.youtube.com/watch?v=_9unR083OPY)
- [Written Guide](https://kitronik.co.uk/blogs/resources/arduino-based-rfid-box-lock)
- [Written Guide](https://the-diy-life.com/arduino-based-rfid-door-lock-make-your-own/)
