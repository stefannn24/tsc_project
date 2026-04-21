InkTime Smartwatch

Hardware Functionality
Power Management

The power path begins at the USB-C connector (5V VBUS), which feeds the Li-Po charge management IC. This IC handles the safe charging cycle for the 250mAh battery. To ensure the MCU and E-paper display receive a clean and stable voltage even as the battery discharges, a DC/DC Buck/Boost regulator is utilized to provide a constant 3.3V system rail.
Compute & Connectivity

The system is driven by the nRF52840 SoC. It manages:

- I2C Bus: Used for communicating with the ultra-low-power IMU (Accelerometer).
- SPI Bus: Dedicated specifically to the E-paper display to ensure enough bandwidth for screen refreshes without interrupting other peripherals.
- USB: Routed directly to the nRF52840 for potential firmware flashing and USB-CDC communications.
- RF: A 50-ohm matched RF trace connects the MCU to a 2.4GHz Johanson SMD chip antenna for Bluetooth Low Energy (BLE) connectivity.

Peripherals

- Display: A low-power E-paper display module.
- IMU: An accelerometer is used for hardware-level step counting.
- Haptics

During the layout and routing phases of the PCB, several specific design rules and constraints were strictly applied to ensure manufacturability and signal integrity:

- Strict top-layer placement: To comply with manufacturing assembly constraints, 100% of the components were placed exclusively on the Top layer.
- Trace width constraints for power: All power delivery networks (VCC, VBUS, 3V3, VBAT) were manually routed using a minimum trace width of 0.3mm. This ensures adequate current handling, especially during peak loads from the shaker motor. Data signals were routed at 0.15mm.
- Antenna keepout zone: The 2.4GHz SMD antenna was placed strictly on the outer edge of the PCB. A complete keepout area was enforced underneath the antenna on all layers.
- Decoupling proximity: All 100nF (0201 package) decoupling capacitors were placed as physically close to the nRF52840 and IMU power pins as mechanically possible to filter out high-frequency switching noise.


(The complete machine-readable .bom and .cpl files are located in the /Manufacturing directory).

License
This project is licensed under the MIT License. See the LICENSE file for details.