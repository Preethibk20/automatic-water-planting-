// Declaration of variable to store water level status
int water; // random variable to store water status from the soil sensor.
void setup () {
// Setup the pins
pinMode (3, OUTPUT); // Set pin 3 as an output to control the relay board.
pinMode (6, INPUT); // Set pin 6 as an input to read the soil sensor.
}
void loop () {
// Read the value coming from the soil sensor
water = digitalRead (6); // If water level is full, the sensor sends a HIGH signal
// If the water level is high (soil is wet), turn off the relay
if (water == HIGH)
digitalWrite (3, LOW); // Turn off the relay (LOW = no signal to relay)
}
else {
// If the water level is low (soil is dry), turn on the relay to water the plants
digitalWrite (3, HIGH); // Turn on the relay (HIGH = provide signal to relay)
}
// Wait for 400 milliseconds before the next reading
delay (400); // Delay in milliseconds
}
