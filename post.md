# Lab 4: Sensors and Actuators

## Overview and Motivation
This week we'll explore how an Arduino can interact with the external environment, through means of sensors and actuators. Using an ultrasonic sensor and a buzzer actuator, we will design a Distance Detector device that can make different sound frequencies based on the distance between the ultrasonic sensor and an external object. We will walk through the new hardware components introduced first, and the design of the Distance Detector will follow. Let's begin!

## Materials
Like other labs, we will need a breadboard, an Arduino microcontroller, and different colored wires. We also need a Buzzer, an actuator that can be programmed to send out different sound frequencies, as well as an Ultrasonic sensor, which sends out ultrasonic sound waves and based on the sound waves reflected back, determine an object’s proximity to the sensor.

## Design Challenge

### Overview and Requirements
We built a proximity detector that emits a sound whose pitch correlates with the distance to a nearby object. There were a few requirements we needed to meet for a proper **Distance Detector**.

 -  We need to make sure that our device (Distance Detector) should be sensitive to and respond correspondingly to distances that span from vary close (1 cm or less) to a distance of 100 cm (1 meter).

 - We also need to make sure our device emits a sound tone in relation to the distance. For example, we used a low-pitched tone to indicate a far distance (100cm). Similarly, we used a high-pitched tone to indicate a near distance (1 cm or less). This means, we also need to make sure that we are emiting sound in relation to the distance i.e. how far an object is or how close it is, should have different and unique sound tones in relation to one another.

 
### Arduino Code and Explanation



**Code Implementation:** One of the most important part of this **Distance Detector** was to implement the correct Arduino Code written in **C** to make sure it functions as intended and fulfills the requirements of this lab. To write this code, we used the help of the code we implemented previously to make sure our Buzzer and our Ultrasonic Sensor functions properly. 



**C Code For Distance Detector:** This is the following code we used in Arduino IDE, comments are added as explanations for what the line of code does:



// Define buzzer and ultrasonic sensor pins

#define BUZZER_PIN 9 
#define TRIG_PIN 12 
#define ECHO_PIN 11  

void setup() {


  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  



  // Initialize serial communication for debugging
  Serial.begin(9600);
  Serial.println("Distance Detector Initialized");


}


void loop() {


  digitalWrite(TRIG_PIN, LOW); 
  delayMicroseconds(2);  
  digitalWrite(TRIG_PIN, HIGH); 
  delayMicroseconds(10); 
  digitalWrite(TRIG_PIN, LOW); 
  

  // measure the duration of the pulse sent back by the sensor (built in function)
  long duration = pulseIn(ECHO_PIN, HIGH); 


  // Convert duration to distance in cm (speed of sound is 0.034 cm/microsecond)
  int distance_cm = duration * 0.034 / 2; 
  
  // Check if distance measurement is valid (within range)
  if (distance_cm > 0 && distance_cm <= 100) {


    // map = (value, fromLow, fromHigh, toLow, toHigh). range from low to high = range to low, to high.
    int frequency = map(distance_cm, 1, 100, 5000, 500); // Adjust frequency range as needed
    

    tone(BUZZER_PIN, frequency);

  
    // Print distance and frequency for debugging
    Serial.print("Distance: ");
    Serial.print(distance_cm);
    Serial.print(" cm, Frequency: ");
    Serial.println(frequency);


  } else {

    Serial.println("Error: Distance measurement out of range");
  }
  
  // Add delay between readings
  delay(500);
}


![Picture of the Code](resources/C-Code-DistanceDetector.png)

### Wiring Steps
**Steps:** 

### Testing

## Conclusion
Sensors and Actuators are essential components of any hardware design since they determine how a machine interacts and responses to external factors from the environment. This design challenge gave us a glimpse of how to leverage these devices, as well as how useful they are.