InkTime Smartwatch

Hardware Functionality
Power Management

The power path begins at the USB-C connector (5V VBUS), which feeds the Li-Po charge management IC. This IC handles the safe charging cycle for the 250mAh battery. To ensure the MCU and E-paper display receive a clean and stable voltage even as the battery discharges, a DC/DC Buck/Boost regulator is utilized to provide a constant 3.3V system rail.
Compute & Connectivity

The system is driven by the nRF52840 SoC. It manages:

I2C Bus: Used for communicating with the ultra-low-power IMU (Accelerometer).
SPI Bus: Dedicated specifically to the E-paper display to ensure enough bandwidth for screen refreshes without interrupting other peripherals.
USB: Routed directly to the nRF52840 for potential firmware flashing and USB-CDC communications.
RF: A 50-ohm matched RF trace connects the MCU to a 2.4GHz Johanson SMD chip antenna for Bluetooth Low Energy (BLE) connectivity.

Peripherals

Display: A low-power E-paper display module. It retains the image without power, but to completely eliminate quiescent current from the display's internal logic during deep sleep, power gating techniques are considered.
IMU: An accelerometer is used for hardware-level step counting and gesture recognition (e.g., wrist-tilt to wake), sending interrupts to the MCU to wake it from sleep.
Haptics: A coin-style ERM shaker motor driven via a MOSFET and PWM signal provides haptic feedback to the user.

During the layout and routing phases of the PCB, several specific design rules and constraints were strictly applied to ensure manufacturability and signal integrity:

- Strict Top-Layer Placement: To comply with manufacturing assembly constraints, 100% of the components were placed exclusively on the Top layer.
- Trace Width Constraints for Power: All power delivery networks (VCC, VBUS, 3V3, VBAT) were manually routed using a minimum trace width of 0.3mm. This ensures adequate current handling, especially during peak loads from the shaker motor. Data signals were routed at 0.15mm to allow high-density escapes from the BGA/aQFN packages.
- Antenna Keepout Zone: The 2.4GHz SMD antenna was placed strictly on the outer edge of the PCB. A complete keepout area was enforced underneath the antenna on all layers (no copper, no ground planes, no traces) to prevent radiation attenuation. The RF feedline itself contains 0 vias.
- Decoupling Proximity: All 100nF (0201 package) decoupling capacitors were placed as physically close to the nRF52840 and IMU power pins as mechanically possible to filter out high-frequency switching noise.

Note: All passive resistors and standard capacitors are 0201 packages to maximize board density, unless dictated otherwise by voltage/power ratings (e.g., 0402/0603 for main DC/DC passives).
Qty	Component	Device / Package	Description	Product Link
- 1	nRF52840-QIAA-R	aQFN-73	Microcontroller (BLE MCU)	JLC C209671
- 1	2450AT18B100E	1206	2.4GHz RF Chip Antenna	JLC C16506
- 1	USB-C Connector	16-Pin SMD	USB Type-C Receptacle	JLC C165948
- 3	Tactile Switches	3.9x2.9mm SMD	Navigation Buttons	JLC C318884
- 1	3.3V Regulator	DFN/WLCSP	DC/DC Buck-Boost / LDO	JLC C47134
- 1	IMU / Accelerometer	LGA-12	Ultra-low power accelerometer	JLC C111244
- 1	Battery Charger	SMD	Li-Po Charge Controller	JLC C12345
- 1	E-Paper Display	1.54"	200x200px E-Ink Panel	N/A (External)
- 1	Li-Po Battery	250mAh	3.7V Rechargeable Battery	N/A (External)
- 1	Shaker Motor	ERM Coin	Vibration Haptic Motor	N/A (External)

(The complete machine-readable .bom and .cpl files are located in the /Manufacturing directory).

License
This project is licensed under the MIT License. See the LICENSE file for details.