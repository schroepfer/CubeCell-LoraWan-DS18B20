# CubeCell-LoraWan-DS18B20
Heltec CubeCell HTCC-AB01 Dev-Board for LoraWan TTN V3 with DS18B20

You must edit the OTAA parameter for TTN V3!

The Input-Pin for the DS18B20 is GPIO5 on the CubeCell, 
Vext of the CubeCell ist VCC for the DS18B20.
Add a resistor 4.7k between Out and Vcc of the DS18B20.

Here is a 3D-case:
https://www.thingiverse.com/thing:5020697

Here the Payload formatter for TTN:
(it includes fields for output to ThinSpeak)

function decodeUplink(input) {
  var bytes = input.bytes;
  var BatVolt = (bytes[0]<<8 | bytes[1]);
  var tmp = (bytes[2]<<8 | bytes[3]);
  return {
    data: {
    Temperatur: ((tmp-5000)/100),
    Batterie: BatVolt/1000,
    field1: ((tmp-5000)/100),
    field2: BatVolt/1000,
    },
    warnings: [],
    errors: []
  };
}
