
# Runway Management System

This is a prototype of the project which is smart enough to manage the Runway of Aeroplane.

## Components:

Some paramount components we leveraged upon,

* Arduino UNO R3
* LCD Screen 16x2
* BlueTooth
* Temperature and Humidity Sensor - DHT
* UltraSonic Sensor
* LED Bulb
* Buzzer

## Procedure:

* Establish the circuit with above enlisted components.
* Upload the RWS.ino code in the Board.
* Test its functionality by moving any object (in our case it is a plane) near UltraSonic sensor.
* Here, the UltraSonic is deployed to measure the distance between plane and the ground, distance numerals are displayed on the screen in rounded figures namely, **50**, **40**, **30**, **20**, **Approaching Minimum** and **Successful**.
* We will cross the land of the flight by contacting plane via BlueTooth.
* If it is **Successful**?, a green LED glows. [Actually we are passing on some queries regarding landing of the flight by an Android app called **AMR Voice**.]
* Buzzer is beeped if there are any climatic fluctuations during landing and hence it is defered. 

## Important Validations

* This Humidity & Temperature check for the fluctuations in the climate. As climate plays the radical role in deciding whether the plane has to landed nearby or continue flying.
* Here, this condition decides this action of the plane,
```
if (humidity < 40 && temperature < 12) {
    lcd.setCursor(0, 0);
    lcd.print("Land your Plane");
    lcd.setCursor(5, 1);
    lcd.print("nearby");
  } else {
    saferunway();
  }
```
* We have also used bluetooth to its max. Voice control, this checks whether the mission is complete or not.
```
if (distance < 6 && distance >= 0) {
    voiceyBT();
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Successful");
  }

void voiceyBT() {
  while (Serial.available()) {
    delay(10);
    char chr = Serial.read();
    if (chr == '#') {
      break;
    }
    voice += chr;
  }
  int len = voice.length();
  if (len > 0) {
    if (voice == "*landed") {
      digitalWrite(led, HIGH);
    } else if (voice == "*okay") {
      digitalWrite(led, LOW);
    }
  }
  voice = "";
}
```
By glowing green LED bulb.

## Significance

* Climatic fluctuations and vagaries are measured and calculated to perform the tasks.
* Distance is accurately counted.
* Check whether plane is landed by bluetooth stimuli and generate respective responds.


