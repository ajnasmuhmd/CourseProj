# CourseProject

code: /*
  This program makes the Arduino measure distance
  in centimeters using an ultrasonic sensor.
  
  Depending on the measured distance, it turns on
  different LEDs to indicate alert zones.
*/

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  // Set trigger pin as output
  pinMode(triggerPin, OUTPUT);

  // Clear the trigger pin
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);

  // Send a 10 microsecond pulse
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);

  // Set echo pin as input
  pinMode(echoPin, INPUT);

  // Read the echo pin and return the sound wave travel time
  return pulseIn(echoPin, HIGH);
}

void setup()
{
  // Buzzer pin
  pinMode(0, OUTPUT);

  // Start serial communication
  Serial.begin(9600);

  // LED pins
  pinMode(10, OUTPUT);
  pinMode(9, OUTPUT);
  pinMode(8, OUTPUT);
}

void loop()
{
  // Play a sound at 523 Hz (C5 note)
  tone(0, 523, 1000);

  // Measure distance in centimeters
  float distance = 0.01723 * readUltrasonicDistance(5, 4);

  // Print distance to Serial Monitor
  Serial.println(distance);

  // Alert zones based on distance
  if (distance < 70) {

    // Close object -> Red alert LED
    digitalWrite(10, HIGH);
    digitalWrite(9, LOW);
    digitalWrite(8, LOW);

  } else if (distance < 150) {

    // Medium distance -> Yellow warning LED
    digitalWrite(10, LOW);
    digitalWrite(9, HIGH);
    digitalWrite(8, LOW);

  } else {

    // Far distance -> Green safe LED
    digitalWrite(10, LOW);
    digitalWrite(9, LOW);
    digitalWrite(8, HIGH);
  }

  // Small delay for stability
  delay(10);
}

i have attached the photos
