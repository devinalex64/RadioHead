# RFM95-LoRa-MAX32620FTHR-Arduino-Examples
This repo contains examples for working with the RFM95 LoRa module using a MAX32620FTHR board in the Arduino IDE. 


# Getting Started
This set of programs is meant to help you get started prototyping with a sx1276 enabled radio board, [Adafruit RFM95W LoRa Radio Transceiver Breakout - 900 MHz](https://www.adafruit.com/product/3072) and [Adafruit LoRa Radio FeatherWing - RFM95W 900 MHz](https://www.adafruit.com/product/3231). This list of programs are meant to work with the Arduino IDE and the [MAX32620FTHR](https://www.maximintegrated.com/en/products/microcontrollers/MAX32620FTHR.html) MCU. This specific set of programs will work with the listed Micro Controller Units (MCUs) with the given pin diagrams below, without modifications necessary to the main program.

## Configuring the LoRa Radio

### Choosing the Correct Frequency
These programs are written with a fork of Adafruits Radiohead librarys compatible with RFM95 LoRa 900MHz Radio modules. The radio's frequency is able to be tuned dynamically, however this program configures the frequency by programming registers at device power on. The 900MHz module supports both 868MHz and 915MHz operation. **Check local laws for which band around 900MHz is set aside for the scientific, commercial, and/or license free usage in your country.**

Make sure that after you configure the Radio to the same frequency that is used in your local area. **THE DEFAULT FREQUENCY SELECTED BY THE INITIALATION FOR A RFM95 RADIO IS 433MHz.** If you are using either a 868MHz or a 900MHz radio you will need to make sure that you call the function below somewhere in the setup() **AFTER** the radio is initialized.

**Exmple setup of the library with the MAX32620FHTR**

```
#include <RH_RF95.h>
#include <SPI.h>

// Singleton instance of the radio driver is done before setup() is called
RH_RF95 radio(SPI_SS_PIN , INTERUPT_0); //Fill in with correct pins

void setup() {
  // For 915MHz Regions use this line, and comment 868MHz setup out
  radio.setFrequency(915.0); // this is MHz

  // For 868MHz Regions use this line, and comment 915MHz setup out
  radio.setFrequency(868.0); // this is MHz

  /*
  Other setup info goes here
  */
}

void loop()
{
  // Main program code here
}
```

Please chose a supported frequency above that is compatible with your RFM95 (or likewise single band compatible sx1276 radio) module.

## Wiring
These program is aimed at working without modifications with RFM95W LoRa 900MHz modules in both a [Breakout board](https://www.adafruit.com/product/3072) or a [FeatherWing](https://www.adafruit.com/product/3231) version.

**Note:** The default pin configurations for the radio in these programs match the wiring diagrams provided. 

### FeatherWing setup
This wiring diagram is useful if your RFM95W LoRa 900MHz module is a Feather wing made by Adafruit.

**Before jumpers are soldered in:**

![feather_pinouts](https://user-images.githubusercontent.com/12534456/41125881-9d9bc9ee-6a5a-11e8-9f1b-2be7af252a4b.jpg)


**After jumpers are soldered in:**

![rfm95_feather_pinouts_drawn_in](https://user-images.githubusercontent.com/12534456/41125880-9b388d40-6a5a-11e8-8d99-ce34b21f5cfe.jpg)


For More information, a detailed wiring guide for the RFM95W Featherwing can be found [here](https://learn.adafruit.com/radio-featherwing/pinoutsc).


### Breakout Board
For a breakout board, the following wiring diagram will work with both the MAX32630FTHR and the MAX32630FTHR mbed boards if wired in the same locations:


**Before the RFM95W is connected with wires:**

![rfm95_breakout_pinouts](https://user-images.githubusercontent.com/12534456/41125877-9b03446e-6a5a-11e8-9772-320f06f9d7d3.jpg)

**After the RFM95W is connected with wires:**

![rfm95_breakout_pinouts_drawn_in](https://user-images.githubusercontent.com/12534456/41125878-9b1f364c-6a5a-11e8-812d-60e4672ff83e.jpg)


For More information, a detailed wiring guide for the RFM95W Breakout Board can be found [here](https://learn.adafruit.com/adafruit-rfm69hcw-and-rfm96-rfm95-rfm98-lora-packet-padio-breakouts/pinouts).

## Antenna

Since this is radio communication, we are going to need antennas to be attached to both of the Radios used in these examples. 

For more information on how to solder an antenna to the RFM95, please click [here](https://learn.adafruit.com/radio-featherwing/assembly).
