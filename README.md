# Arduino Nano EMF Meter (Electric Field Detector)

An embedded C++ application for an **Electric Field (EMF) Detector** built using an **Arduino Nano** micro-controller. This handheld device samples electromagnetic frequencies through an analog antenna probe, processes the signal logic, and provides real-time visual and audio feedback based on field intensity.

## 🚀 Key Features

* **Real-Time Signal Processing:** Samples raw electromagnetic data from an analog antenna pin (`A0`) and implements time-buffered averaging (`CHECK_DELAY`) to filter transient signal noise.
* **Dynamic OLED GUI Display:** Powered by the Adafruit SH1106 library to drive a 128x64 I2C OLED screen. Features a custom splash screen logo mapped via a Flash-optimized PROGMEM byte matrix (`matrica`), standard text readouts, and a smooth, dynamically mapped horizontal progress bar.
* **Multi-Tier Audio Alerts:** Multi-level frequency feedback mapped via the hardware `tone()` function on pin `12` to notify the user of unsafe EMF thresholds (100Hz, 500Hz, and 1000Hz alert steps).
* **Low Memory Footprint:** Utilizes the `PROGMEM` keyword to store graphical bitmap arrays natively inside Flash memory, preventing SRAM overflow on the ATmega328P chip.

---

## 🛠️ Hardware Requirements

* **Microcontroller:** Arduino Nano (or any ATmega328P based board)
* **Display:** SH1106 I2C OLED Display (128x64 pixel resolution)
* **Sensing Probe:** Copper wire/telescopic antenna connected to Analog Pin `A0`
* **Audio Indicator:** Piezo Buzzer / Speaker connected to Digital Pin `12`

---

## 📂 Code Architecture & Execution

The firmware logic flows through three main phases:

1. **`setup()`**: Initializes I2C wire communication, configures hardware pin states, and executes the splash sequence by printing the custom bitmap matrix and project descriptors ("EMF METER").
2. **`loop()`**: Continuously checks electromagnetic interference, computes a non-blocking running average, and dynamically scales the graphic progress bar (`map()` constraint function).
3. **`showReadings()`**: Updates the text canvas buffer to print calculated numerical values directly onto the I2C bus.

---

## 🔧 Software Libraries Used

To compile this project inside the Arduino IDE, ensure you have the following packages installed:
* `Wire.h` (Built-in I2C driver)
* `SPI.h` (Built-in SPI interface bus)
* `Adafruit_GFX.h` (Core graphics rendering framework)
* `Adafruit_SH1106.h` (Specific hardware driver for the OLED display panel)
