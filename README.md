# light-sensor-night-light

## What is it?

This project is an automatic night light built using an Arduino Uno, a photoresistor (LDR), and an LED. The system detects the amount of light in the environment and automatically turns the LED on when it gets dark and turns it off when the area is bright.

The goal of this project was to learn how Arduino can use sensor data to make decisions without needing a manual input like a button.


## Components Used

* Arduino Uno R3
* Breadboard
* (1)yellow LED
* 220Ω resistor (for LED protection)
* Photoresistor (LDR / light sensor)
* 10kΩ resistor (for voltage divider)
* (3)Jumper wires
* Arduino IDE


## How It Works

The photoresistor changes its resistance depending on the amount of light hitting it. It is combined with a 10kΩ resistor to create a voltage divider, allowing the Arduino to measure the light level through analog pin **A0**.

The Arduino reads the sensor value using `analogRead()` and receives a number between **0 and 1023**. Based on that value, the Arduino decides whether the LED should turn on or off.

* Low light level → LED turns ON
* High light level → LED turns OFF

The LED is controlled through digital pin **D9**.


## Challenges/what i got stuck on/wondered throughout the build


* Understanding the difference between digital inputs and analog inputs
* Learning how a photoresistor changes resistance based on light
* Understanding why a voltage divider is needed to read the sensor value
* Adjusting the sensor threshold because different lighting conditions produce different readings


## How I Solved Them

I tested each part of the circuit separately and using the Serial Monitor to see the sensor readings.

By covering the photoresistor and shining light on it, I was able to see how the values changed. Then i would adjust the code's threshold value so the LED would turn on at the correct darkness level.


## What I Learned

* The difference between digital and analog signals
* How Arduino reads sensor values using analog pins
* How photoresistors work and how they can be used to detect environmental changes
* How voltage dividers allow sensors to communicate with microcontrollers
* How to use the Serial Monitor for debugging
* How to create systems that respond to real world conditions
* The importance of calibrating sensors instead of assuming they will have a fixed value

## Exact code i used
int lightSensor = A0;
int ledPin = 9;

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  int lightLevel = analogRead(lightSensor);

  Serial.println(lightLevel); // lets you see the light value

  if (lightLevel < 500) {  // darker than this = turn on LED
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }

  delay(100);
}


## Future Improvements

* Add a potentiometer to manually adjust the brightness threshold
* Use PWM to make the LED gradually fade in and out
* Add multiple LEDs for just more lighting
