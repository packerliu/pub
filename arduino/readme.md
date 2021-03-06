# Arduino Steps

Follow the instruction in [Workshop: Build a TTN LoRaWAN Node](https://github.com/kersing/node-workshop/blob/master/lora32u4.md):

1. Install [Arduino IDE](https://www.arduino.cc/en/Main/Software)
2. Adding "Adafruit AVR Boards" from "Tools -> Board Manager", then choose "Adafruit Feather 32U4"
3. Get the LMIC library, https://github.com/matthijskooijman/arduino-lmic
4. Get the low power library, https://github.com/rocketscream/Low-Power
5. Create a TTN account
6. Create an Application under TTN Console, using following variables:
    - Application ID : ucite
    - Description : "Low Power Long Range Serial Link"
Application EUI : leave empty, the value will be generated.
Handler registration : choose 'ttn-handler-us-west'.
7. Click "Add Application" to create one.
8. Receive App EUI as  "70B3D57ED001DB5C". Todo: hiding this.
9. Adding a Node, using device name: "ard01".  Then we can see it at https://console.thethingsnetwork.org/applications/ucite/devices/ard01
10. Creating the Arduino sketch, from sample at  https://raw.githubusercontent.com/kersing/node-workshop/master/lora32u4-sketch/lora32u4-sketch.ino
11. To 'tune' this example to your TTN application you need to change:
    - DEVEUI:
    - APPEUI:
    - APPKEY:
12. wiring difference between V1.2 and 1.1/1.0, https://www.thethingsnetwork.org/forum/t/big-lora32u4-boards-topic/15273

13. Arduino Manual Bootloading to fix IDE issue, https://learn.adafruit.com/adafruit-feather-32u4-adalogger/using-with-arduino-ide

14. Also adjust the clock tolerance to 10% instead of 1% at ```initfunc()``` with:
```c
// initial job
static void initfunc (osjob_t* j) {
  // reset MAC state
  LMIC_reset();
  LMIC_setClockError(MAX_CLOCK_ERROR * 10 / 100);
  // start joining
  LMIC_startJoining();
  // init done - onEvent() callback will be invoked...
}
```

15. LoRa32u4 II v1.2 is different pin at http://iotbyskovholm.dk/?q=content/lora32u4-ii-v12-development-board

# RPi3+Dragino Lora HAT

1. LoRa - Raspberry Pi - Single Channel Gateway - Cheap!, https://www.hackster.io/ChrisSamuelson/lora-raspberry-pi-single-channel-gateway-cheap-d57d36
2. Make it a systemctl service, https://medium.com/@benmorel/creating-a-linux-service-with-systemd-611b5c8b91d6
3. Enable these services, https://www.linode.com/docs/quick-answers/linux/start-service-at-boot/

3. Good article to read/review LoRa, https://medium.com/coinmonks/lpwan-lora-lorawan-and-the-internet-of-things-aed7d5975d5d
4. Enable GPS +RPi3 at https://wiki.dragino.com/index.php?title=Getting_GPS_to_work_on_Raspberry_Pi_3_Model_B
5. Install Dual Channel forwarder, https://github.com/bokse001/dual_chan_pkt_fwd

6. Dual-Chan Gateway with Raspberry PI3 + Dragino Hat v1.4 and Downstream messages, https://www.thethingsnetwork.org/forum/t/dual-chan-gateway-with-raspberry-pi3-dragino-hat-v1-4-and-downstream-messages/13284
