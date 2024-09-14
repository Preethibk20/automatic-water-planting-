onst int relayPin = 3; // Output pin for controlling the relay
const int sensorPin = 6; // Input pin from the soil moisture sensor
const unsigned long debounceDelay = 400; // Delay to debounce sensor readings

bool lastSensorState = LOW; // Last state of the soil sensor
unsigned long lastDebounceTime = 0; // Last time the sensor state changed

void setup() {
  pinMode(relayPin, OUTPUT); // Set the relay pin as OUTPUT
  pinMode(sensorPin, INPUT); // Set the sensor pin as INPUT
  digitalWrite(relayPin, LOW); // Ensure the relay is initially off
}

void loop() {
  int currentSensorState = digitalRead(sensorPin); // Read the current state of the sensor

  // Check if the sensor state has changed
  if (currentSensorState != lastSensorState) {
    lastDebounceTime = millis(); // Reset debounce timer
  }

  // Check if enough time has passed since the last change
  if ((millis() - lastDebounceTime) > debounceDelay) {
    // Only update the relay state if the sensor state has stabilized
    if (currentSensorState == HIGH) { // If soil is moist
      digitalWrite(relayPin, LOW); // Turn off the relay
    } else { // If soil is dry
      digitalWrite(relayPin, HIGH); // Turn on the relay
    }
  }

  lastSensorState = currentSensorState; // Update the last sensor state
}
