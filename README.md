# ESP32-Circuit-Design-and-Simulation
# Introduction

The circuit presented below is built using the ESP32 micrcontroller via Wokwi.


__Purpose:__ to control an LED's state by pressing the pushbutton. The push button is an ideal electronic component for its ease of operation, reliability, fast response time, visual feedback, and adaptability. Additionally, it allows the LED to not be on all the time which makes it cost-effective and energy-saving too.

# My circuit
<img width="1373" alt="Screenshot 2024-07-13 at 10 59 33 PM" src="https://github.com/user-attachments/assets/cc13b8f3-d9a2-44ef-ad23-a57b128543ab">

__Components:__ ESP32, 1 LED, 1 pushbutton, resistor, internal pull up resistor, wires.

__Structure:__ I started off my connecting both electronic components (LED and pushbutton) to ground. I connected the upper leg of the pushbutton to the digital pins and the LED's longer leg (anode) to a digital pin with a resistor to prevent extra current that can burn out the LED. I also connected the electric board to the 5V pin to provide the elctronic components with a power supply.
 
# Code
``` cpp
// Define GPIO pins connected to LED and Pushbutton
const int ledPin = 13;      // GPIO 13 for LED
const int buttonPin = 12;   // GPIO 12 for Pushbutton

// Variables to store the current state
bool LED_ON = false;
bool buttonPressed = false;

void setup() {
  Serial.begin(115200);
  // Initialize GPIO pins
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT_PULLUP); // Enable internal pull-up resistor for the pushbutton
}

void loop() {
  // Read the state of the pushbutton
  bool buttonState = digitalRead(buttonPin);
  
  // Check if the pushbutton is pressed (active LOW due to pull-up)
  if (buttonState == LOW && !buttonPressed) {
    buttonPressed = true;
    Serial.println("Button pressed.");
    delay(100); // Debounce delay

    // Toggle the LED state based on button press
    if (!LED_ON) {
      Serial.println("LED ON");
      digitalWrite(ledPin, HIGH);
      LED_ON = true;
    } else {
      Serial.println("LED OFF");
      digitalWrite(ledPin, LOW);
      LED_ON = false;
    }
  } else if (buttonState == HIGH) {
    buttonPressed = false;
  }
}
```
__Why did I use an internal pullup resistor in my code?__ Because it simplifies the circuit and eliminates the need of an external one, which also means easier wiring, and it can be easily enabled or disabled in software, and that eases modifying the circuit without modifying the hardware connections.

# Try my circuit out yourself!
__Project Link__:
(https://wokwi.com/projects/403325131488429057)
