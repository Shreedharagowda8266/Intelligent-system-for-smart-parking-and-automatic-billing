**RFID BASED SMART PARKING SYSTEM**

**AIM:**
The aim of the project, IOT based fully automated parking system for vehicle parking stations implemented by microcontroller and the RFID module. The main aim of this project is reduces human interaction in parking area.

**OBJECTIVE:**
Optimizing Parking Space: Efficiently manage available parking spots by providing real-time data on available spaces and guiding drivers to open spots. This minimizes time spent searching for parking and reduces congestion.

Enhancing User Experience: Offer a seamless experience for drivers by providing user-friendly interfaces or apps that allow them to easily find parking, reserve spots, and navigate to their designated space.

Real-Time Monitoring: Employ sensors or cameras to monitor parking spaces in real time, allowing for accurate information on available spots and enabling immediate updates for drivers.

Automatic Billing: Implement a system that calculates parking fees based on duration and automatically bills users through various payment methods (e.g., credit card, mobile payment) upon exiting the parking area.

Integration and Accessibility: Ensure compatibility with different devices and platforms, making the system accessible to a wide range of users. Integration with navigation apps or in-car systems can further streamline the parking process.

Security and Safety: Employ measures to ensure the safety of vehicles and users within the parking area, including surveillance, emergency assistance features, and secure payment transactions.

Data Analysis and Optimization: Utilize data collected from the system to analyze parking patterns, peak times, and user behavior, enabling better resource allocation and future planning.

**COMPONENTS REQUIRED:**
Arduino uno
20*4 LCD display
12C LCD module
Mini servomotor SG-90
IR sensor
Jumper cable
Bread board
5V 2amp power adapter
Adafruit metro ESP32-S2

**WORKING:**
•	To implement an intelligent system for real-time parking , you need a combination of hardware and software components.
•	Use sensors, cameras, or IoT devices to monitor each parking space in real-time.Employ image recognition or machine learning algorithms to identify whether a space is occupied or vacant.
•	Establish a reliable communication network to connect all the parking space sensors to a central server.Ensure low-latency communication for real-time updates.
•	Set up a centralized server that receives and processes data from parking space sensors.Implement algorithms to aggregate and analyse the data to determine parking space availability.
•	Implement a reservation system that allows users to reserve a parking space for a specific duration.

**FLOW CHART:**
![WhatsApp Image 2023-11-24 at 9 59 21 AM](https://github.com/Shreedharagowda8266/Intelligent-system-for-smart-parking-and-automatic-billing/assets/119619029/e644097c-155b-4628-b276-2ed3a7223002)

**MIND MAP:**
![WhatsApp Image 2023-11-24 at 9 59 21 AM (1)](https://github.com/Shreedharagowda8266/Intelligent-system-for-smart-parking-and-automatic-billing/assets/119619029/7231a3d2-2149-4217-9a6a-4146af9dd012)

**Circuit diagram:**
![WhatsApp Image 2023-11-22 at 4 40 03 PM](https://github.com/Shreedharagowda8266/Intelligent-system-for-smart-parking-and-automatic-billing/assets/119619029/94328aa2-ea1d-4ab1-a2e0-06584f22c34f)

**BLOCK DIAGRAM:**
![WhatsApp Image 2023-11-25 at 8 58 46 PM](https://github.com/Shreedharagowda8266/Intelligent-system-for-smart-parking-and-automatic-billing/assets/119619029/9103a866-0e9c-4b6a-bc90-b5972fca3fff)

**APPLICATION:**
Real-Time Parking Management: Sensor Integration: Install sensors in parking spots to detect vehicle presence. These sensors can be ultrasonic, infrared, or camera-based.

Data Collection: Sensors relay real-time data to a central system, indicating which parking spots are vacant or occupied.

Machine Learning for Prediction: Algorithms can analyze patterns in parking data to predict peak hours, helping optimize operations.

Mobile App or Interface: Users can access an app or interface showing available parking spaces in real-time, guiding them to empty spots.

Automated Guidance: Once a user selects a spot, the system can provide navigation to that spot through the app.

**ALGORITHM:**
 Initialize RFID module, LCD display, servo motor, and IR sensor pins.
2. Set up LCD columns and rows.
3. Initialize RFID module and print a welcome message on the LCD.
4. Attach the servo motor to its pin.

5. Define parking variables:
•	Total Spaces = 4
•	Available Spaces = 4

6. Setup function:
•	Begin LCD and serial communication.
•	Initialize SPI bus for RFID.
•	Initialize RFID module.
•	Print system initialization message on the LCD.
•	Attach the servo motor.

7. Loop function:
•	Check if a new RFID card is present.
•	If a card is present, read card details and print the name on the serial monitor.
•	Authenticate and read the first name and the last name from the RFID card.   
•	Halt the RFID module and update the parking status.
•	Display parking status on the LCD.

8. Update Parking Status function:
•	Read IR sensor inputs.
•	If the fifth sensor is HIGH, move the servo motor to 90 degrees; otherwise, move it to 0 degrees.
•	Update available spaces based on IR sensor inputs.
•	Ensure available spaces are within the valid range (0 to totalSpaces).

9. Display Parking Status function:
•	Clear the LCD.
•	Iterate over each parking space:
•	Print space number and status (Available/Occupied) on the LCD.

10. End

**CODE:**

    #include <Servo.h>
    #include <MFRC522.h>
    #include <SPI.h>
    #include <LiquidCrystal.h>
    #define SS_PIN 10
    #define RST_PIN 9

    // Pin configuration for the LCD
     const int rs = 8;
     const int en = 7;
     const int d4 = 5;
     const int d5 = 4;
     const int d6 = 3;
     const int d7 = 2;
    // Pin configuration for IR sensors
     const int irSensorPin1 = A0;
     const int irSensorPin2 = A1;
     const int irSensorPin3 = A2;
     const int irSensorPin4 = A3;
     Servo servoMotor;
     const int servoPin=6;

     // Create an LCD object
     LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

     // Parking variables
      int totalSpaces = 4;
      int availableSpaces = 4;
      MFRC522 mfrc522(SS_PIN,RST_PIN);
      void setup() {

     // Set up the LCD columns and rows
       lcd.begin(20, 4);
       Serial.begin(9600);
       SPI.begin();
       mfrc522.PCD_Init();
       
      // Simulate initialization of parking system
        lcd.print("Smart Parking");
        delay(2000);
        lcd.clear();
        servoMotor.attach(servoPin);
        Serial.println("put your card to the reader");
        Serial.println();
        }

       void loop(){

        // Simulate updating parking status
        updateParkingStatus();
        // Display parking status on the LCD
           displayParkingStatus();
        // Your main code for real-time updates can go here
         delay(1000);  // Update every 1seconds
         }

      void updateParkingStatus() {

       // Read IR sensor inputs
  
        int irSensorValue1 = digitalRead(irSensorPin1);
        int irSensorValue2 = digitalRead(irSensorPin2);
        int irSensorValue3 = digitalRead(irSensorPin3);
        int irSensorValue4 = digitalRead(irSensorPin4);

          if ( ! mfrc522.PICC_IsNewCardPresent()) 
          {
          return;
          }
  
          // Select one of the cards
        
          if ( ! mfrc522.PICC_ReadCardSerial()) 
          {
          return;
          }
  
         //Show UID on serial monitor
         
         Serial.print("UID tag :");
         String content= "";
         byte letter;
         for (byte i = 0; i < mfrc522.uid.size; i++) 
        {
         Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
         Serial.print(mfrc522.uid.uidByte[i], HEX);
         content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
         content.concat(String(mfrc522.uid.uidByte[i], HEX));
         }
         Serial.println();
         Serial.print("Message : ");
         content.toUpperCase();
        
        //change here the UID of the card/cards that you want to give access
        if (content.substring(1) == "03 89 5E 2F") 
       {
       Serial.println("Authorized access");
       Serial.println();
       delay(500);
       servoMotor.write(90);
       delay(5000);
        servoMotor.write(0);
       }
        else   {
        Serial.println(" Access denied");
      }

     // Adjust available spaces based on IR sensor inputs
      availableSpaces = totalSpaces;
      if (irSensorValue1 == LOW) {
     availableSpaces--;
      }
       if (irSensorValue2 == LOW) {
       availableSpaces--;
      }
      if (irSensorValue3 == LOW) {
      availableSpaces--;
     }
      if (irSensorValue4 == LOW) {
      availableSpaces--;
     }
     
    // Ensure available spaces do not go below 0
      availableSpaces = constrain(availableSpaces, 0, totalSpaces);
     }
 
    void displayParkingStatus() {
    lcd.clear();

    for (int i = 0; i < totalSpaces; ++i) {
    lcd.setCursor(0, i );
    lcd.print("Space ");
    lcd.print(i + 1);
    lcd.print(": ");

    if (i < availableSpaces) {
      lcd.print("Available");
    } else {
      lcd.print("Occupied");
    }
    }
    }

**RESULT:**
![WhatsApp Image 2023-11-24 at 10 12 21 AM](https://github.com/Shreedharagowda8266/Intelligent-system-for-smart-parking-and-automatic-billing/assets/119619029/2448470c-44cf-4f13-b07e-3d95a0330604)

**DEMO VIDEO:**
https://github.com/Shreedharagowda8266/Intelligent-system-for-smart-parking-and-automatic-billing/assets/119619029/759ad39d-f557-46e5-b0e7-42fb0685d980








