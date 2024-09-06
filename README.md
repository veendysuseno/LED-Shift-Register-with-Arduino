# LED Shift Register with Arduino

This project demonstrates how to control an 8-segment LED display using a shift register (e.g., 74HC595). The code sequentially lights up each LED one at a time, creating a running light effect.

## Components Used

- Arduino Uno
- 74HC595 Shift Register
- 8 LEDs
- 8 Resistors (220Ω recommended for each LED)
- Jumper wires
- Breadboard

## Pin Configuration

- **DATA_PIN**: connected to the data input of the shift register (Pin 8).
- **LATCH_PIN**: connected to the latch pin of the shift register (Pin 9).
- **CLOCK_PIN**: connected to the clock pin of the shift register (Pin 10).

## How It Works

- The Arduino sends serial data to the shift register, which controls the LEDs.
- The `for` loop in the `loop()` function cycles through each LED, turning them on one at a time.
- The `bitSet()` function is used to set the appropriate bit for each LED.
- The shift register is updated by toggling the clock and latch pins.

## Code

```cpp
const int DATA_PIN  = 8;
const int LATCH_PIN = 9;
const int CLOCK_PIN = 10;

void setup() {
    pinMode( DATA_PIN, OUTPUT );
    pinMode( LATCH_PIN, OUTPUT );
    pinMode( CLOCK_PIN, OUTPUT );
}

void loop() {
    for( int i = 0; i < 8; i++ ) {
        byte leds = 0;
        bitSet( leds, i );
        digitalWrite( LATCH_PIN, LOW );

        for( int j = 0; j < 8; j++ ) {
            digitalWrite( DATA_PIN, leds & (1 << j) );
            digitalWrite( CLOCK_PIN, LOW );
            digitalWrite( CLOCK_PIN, HIGH );
        }

        digitalWrite( LATCH_PIN, HIGH );
        delay( 200 );
    }
}
```

## How to Use

1. Connect the shift register to the Arduino and LEDs as described in the pin configuration.
2. Upload the provided code to the Arduino.
3. Watch as each LED lights up in sequence.

## Features

- Sequentially lights up each LED using a shift register.
- Simple demonstration of controlling multiple LEDs with minimal Arduino pins.
- Useful for learning about serial communication with shift registers.
