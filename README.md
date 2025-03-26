# Embedded-systems

## Project 1 
### Traffic Lights Effect 
- The lights will be flashing, Red -> Red -> Yellow -> Green
```cpp
const int numTrafficLeds = 3;

// Pin 2: Red, Pin 3: Yellow, Pin 4: Green
const int trafficLedPins[numTrafficLeds] = {2, 3, 4};

// Define indices within the trafficLedPins array for easier reference
const int redLedIndex = 0;    // Corresponds to pin 2
const int yellowLedIndex = 1; // Corresponds to pin 3
const int greenLedIndex = 2;  // Corresponds to pin 4

// Define states for the traffic light sequence
enum TrafficState {
  STATE_RED,
  STATE_RED_YELLOW,
  STATE_GREEN,
  STATE_YELLOW
};

TrafficState currentState = STATE_RED; // Initial state

// Define durations for each state (in milliseconds)
unsigned long redDuration = 5000;
unsigned long redYellowDuration = 1500;
unsigned long greenDuration = 5000;
unsigned long yellowDuration = 1500;

// --- Variables for millis() based timing ---
unsigned long previousMillis = 0;            // Stores the last time the state changed
unsigned long currentInterval = redDuration; // Interval for the current state

void setup() {
  // Initialize the traffic light LED pins as outputs
  for (int i = 0; i < numTrafficLeds; i++) {
    pinMode(trafficLedPins[i], OUTPUT);
    digitalWrite(trafficLedPins[i], LOW); // Start with all LEDs off
  }

  // Set the initial state (RED light ON)
  digitalWrite(trafficLedPins[redLedIndex], HIGH);
  currentState = STATE_RED;
  currentInterval = redDuration;
  previousMillis = millis(); // Initialize the timer

  // Serial.begin(9600); // Optional: for debugging
  // Serial.println("Starting Traffic Light: RED");
}

void loop() {
  unsigned long currentMillis = millis();

  // Check if it's time to change the state based on the current interval
  if (currentMillis - previousMillis >= currentInterval) {
    // Update the time marker for the next interval
    previousMillis = currentMillis;

    // --- State Transition Logic ---
    switch (currentState) {
      case STATE_RED:
        // Currently RED, transition to RED_YELLOW
        digitalWrite(trafficLedPins[yellowLedIndex], HIGH); // Turn on Yellow
        currentState = STATE_RED_YELLOW;
        currentInterval = redYellowDuration;
        // Serial.println("State: RED+YELLOW");
        break;

      case STATE_RED_YELLOW:
        // Currently RED_YELLOW, transition to GREEN
        digitalWrite(trafficLedPins[redLedIndex], LOW);    // Turn off Red
        digitalWrite(trafficLedPins[yellowLedIndex], LOW); // Turn off Yellow
        digitalWrite(trafficLedPins[greenLedIndex], HIGH); // Turn on Green
        currentState = STATE_GREEN;
        currentInterval = greenDuration;
        // Serial.println("State: GREEN");
        break;

      case STATE_GREEN:
        // Currently GREEN, transition to YELLOW
        digitalWrite(trafficLedPins[greenLedIndex], LOW);  // Turn off Green
        digitalWrite(trafficLedPins[yellowLedIndex], HIGH); // Turn on Yellow
        currentState = STATE_YELLOW;
        currentInterval = yellowDuration;
        // Serial.println("State: YELLOW");
        break;

      case STATE_YELLOW:
        // Currently YELLOW, transition to RED
        digitalWrite(trafficLedPins[yellowLedIndex], LOW); // Turn off Yellow
        digitalWrite(trafficLedPins[redLedIndex], HIGH);   // Turn on Red
        currentState = STATE_RED;
        currentInterval = redDuration;
        // Serial.println("State: RED");
        break;
    }
  } 
}

```

## Project 2 
### Shifting / Trailing Effect
- Two LEDs Switching on and then the behind is trailing
```
// --- Shifting Effect (Knight Rider Style) ---

// Define the total number of LEDs
const int ledCount = 12;

// Define the Arduino pins connected to the LEDs (adjust if needed)
const int ledPins[ledCount] = {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};

// Variables for the shifting effect
int currentLedIndex = 0; // Index of the *first* LED in the currently lit pair

// Define the interval between shifts (in milliseconds) - controls the speed
const unsigned long shiftInterval = 150;

// --- Variables for millis() based timing ---
unsigned long previousMillis = 0; // Stores the last time the shift occurred

void setup() {
  // Initialize all LED pins as outputs
  for (int i = 0; i < ledCount; i++) {
    pinMode(ledPins[i], OUTPUT);
    digitalWrite(ledPins[i], LOW); // Start with all LEDs off
  }
  previousMillis = millis(); // Initialize the timer
  // Serial.begin(9600); // Optional: for debugging
}

void loop() {
  unsigned long currentMillis = millis();

  // Check if it's time to perform the next shift
  if (currentMillis - previousMillis >= shiftInterval) {
    previousMillis = currentMillis; // Reset the timer for the next interval

    // --- Calculate LED indices for the shift ---

    // Determine the index of the LED to turn OFF.
    // This is the one trailing behind the *previous* position of the first LED.
    // Modulo arithmetic handles wrap-around (when currentLedIndex is 0).
    int ledToTurnOff = (currentLedIndex - 1 + ledCount) % ledCount;

    // Determine the indices of the two LEDs to turn ON for the current step.
    int led1ToTurnOn = currentLedIndex;
    int led2ToTurnOn = (currentLedIndex + 1) % ledCount; // Modulo handles wrap-around

    // --- Update the LEDs ---
    digitalWrite(ledPins[ledToTurnOff], LOW);  // Turn off the trailing LED
    digitalWrite(ledPins[led1ToTurnOn], HIGH); // Turn on the first LED of the new pair
    digitalWrite(ledPins[led2ToTurnOn], HIGH); // Turn on the second LED of the new pair

    // --- Advance the position for the next iteration ---
    currentLedIndex = (currentLedIndex + 1) % ledCount; // Move to the next starting LED, wrap around

    // Serial.print("Shifted. Current Index: "); // Optional debugging
    // Serial.println(currentLedIndex);

  } 
}
```

## Project 3
### Morse Code Generation
- Generate a sentence using morse code by lighting LEDs in a specific way, maybe creating your initials using that approach
```
// --- Morse Code Blinker (SOS) ---

// Define the total number of LEDs
const int ledCount = 12;

// Define the Arduino pins connected to the LEDs (adjust if needed)
const int ledPins[ledCount] = {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13};

// --- Morse Code Definitions ---
const unsigned long timingUnit = 200; // Base duration for one 'dot' (milliseconds)
const unsigned long dotDuration = timingUnit;
const unsigned long dashDuration = timingUnit * 3;
const unsigned long intraCharGap = timingUnit; // Gap between dots/dashes within a letter
const unsigned long interCharGap = timingUnit * 3; // Gap between letters (after S, after O)
const unsigned long wordGap = timingUnit * 7;      // Gap after the word "SOS"

// Structure to define a Morse element (ON/OFF state and its duration)
struct MorseElement {
  int state;              // HIGH (ON) or LOW (OFF)
  unsigned long duration; // How long to hold this state
};

// Define the sequence for "SOS" using the structure
// Sequence: . . . (inter) - - - (inter) . . . (word gap)
const MorseElement sosSequence[] = {
  {HIGH, dotDuration}, {LOW, intraCharGap}, // S part 1
  {HIGH, dotDuration}, {LOW, intraCharGap}, // S part 2
  {HIGH, dotDuration}, {LOW, interCharGap}, // S part 3 & gap after S

  {HIGH, dashDuration},{LOW, intraCharGap}, // O part 1
  {HIGH, dashDuration},{LOW, intraCharGap}, // O part 2
  {HIGH, dashDuration},{LOW, interCharGap}, // O part 3 & gap after O

  {HIGH, dotDuration}, {LOW, intraCharGap}, // S part 1
  {HIGH, dotDuration}, {LOW, intraCharGap}, // S part 2
  {HIGH, dotDuration}, {LOW, wordGap}       // S part 3 & word gap after SOS
};

// Calculate the number of elements in the sequence array
const int sequenceLength = sizeof(sosSequence) / sizeof(sosSequence[0]);

// Index to keep track of the current position in the Morse sequence
int sequenceIndex = 0;

// --- Variables for millis() based timing ---
unsigned long previousMillis = 0;            // Stores the last time the state changed
unsigned long currentInterval = 0;           // Stores the duration for the current Morse element

// --- Helper function to set the state of all LEDs ---
void setAllLeds(int state) {
  for (int i = 0; i < ledCount; i++) {
    digitalWrite(ledPins[i], state);
  }
}

void setup() {
  // Initialize all LED pins as outputs
  for (int i = 0; i < ledCount; i++) {
    pinMode(ledPins[i], OUTPUT);
  }

  // --- Initialize for the first element of the sequence ---
  sequenceIndex = 0;
  int initialState = sosSequence[sequenceIndex].state;
  currentInterval = sosSequence[sequenceIndex].duration;
  setAllLeds(initialState); // Set the initial LED state
  previousMillis = millis(); // Initialize the timer

  // Serial.begin(9600); // Optional: for debugging
  // Serial.println("Starting Morse Code: SOS");
}

void loop() {
  unsigned long currentMillis = millis();

  // Check if the duration for the current Morse element has passed
  if (currentMillis - previousMillis >= currentInterval) {
    previousMillis = currentMillis; // Reset the timer for the next interval

    // Move to the next element in the sequence, wrapping around at the end
    sequenceIndex = (sequenceIndex + 1) % sequenceLength;

    // Get the state and duration for this next element
    int newState = sosSequence[sequenceIndex].state;
    currentInterval = sosSequence[sequenceIndex].duration;

    // Apply the new state to all LEDs
    setAllLeds(newState);

    // Serial.print("Morse Index: "); Serial.print(sequenceIndex); // Optional Debugging
    // Serial.print(" State: "); Serial.print(newState == HIGH ? "ON" : "OFF");
    // Serial.print(" Interval: "); Serial.println(currentInterval);

  } // end of timing check

  // --- The rest of the loop is free ---
}
```
