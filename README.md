# PCA9557-arduino

Write & Read digital logic via PCA9557 8-bit I/O expander

## Example

```c++
#include <Arduino.h>
#include <Wire.h>
#include <PCA9557.h>

PCA9557 io(0x19, &Wire); // 0x19 for iFarm4G board

void setup() {
  Serial.begin(115200);
  Wire.begin();

  io.pinModeRegister(0xFF); // Sets all pins as INPUT

  io.pinMode(0, INPUT); // Config IO0 of PCA9557 to INPUT mode
  io.pinMode(1, OUTPUT); // Config IO1 of PCA9557 to OUTPUT mode

  io.writeRegister(0x00); // Sets all pins that are outputs to LOW
  // Serial.println(io.readRegister()); // Reads all the state of all of the inputs
}

void loop() {
  io.digitalWrite(1, HIGH);
  delay(1000);
  io.digitalWrite(1, LOW);
  delay(1000);
  // Serial.println("D0 = " + String(io.digitalRead(0)));
}
```
Be warned the GPIO 0 of the I/O expander is an open-drain output / normal input
