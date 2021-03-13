# Setup Arduino IDE

Tools > Board: "Arduino Nano"

Tools > Processor: "ATmega328P (Old Bootloader)"

Tools > Port: select the right USB port

# Power supply

A CR2032 cell battery is not sufficient to power an Arduino Nano (using Vin and GND), or at least not sufficient to power an RF433 transmitter. Maybe it was just the signal that was too low to be received by the Sonoff RF Bridge?
