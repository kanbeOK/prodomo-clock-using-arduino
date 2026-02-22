# prodomo-clock-using-arduino

# The Components 

* **Arduino Uno** 
* **Active Buzzer** 
* **Tactile Push Button**
* **10k Ohm Resistor** 
* **Jumper wires and Breadboard*



### The Wiring Logic

1. **The Buzzer:** Connect the positive (+) pin to **Digital Pin 8** and the negative (-) pin to **GND**.
2. **The Button:** * Connect one side to **5V**.
* Connect the other side to **Digital Pin 2**.
* Also connect **Pin 2** to **GND** through the **10k Ohm resistor** (this is a pull-down resistor to prevent "floating" signals).



---

#Code



```cpp
// Pins
const int buzzerPin = 8;
const int buttonPin = 2;

// Timing (45 minutes in milliseconds)
const unsigned long studyTime = 45ULL * 60ULL * 1000ULL; 
unsigned long startTime;
bool timerRunning = true;

void setup() {
  pinMode(buzzerPin, OUTPUT);
  pinMode(buttonPin, INPUT);
  startTime = millis(); 
}

void loop() {
  unsigned long currentTime = millis();

  // 1. Check if time is up
  if (timerRunning && (currentTime - startTime >= studyTime)) {
    digitalWrite(buzzerPin, HIGH); 
    timerRunning = false;          
  }

  // 2. Check for button press to reset
  if (digitalRead(buttonPin) == HIGH) {
    digitalWrite(buzzerPin, LOW);  
    startTime = millis();          
    timerRunning = true;           
    delay(500);                    
  }
}

```



