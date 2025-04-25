#### Power-On Reset (POR):
In the Caravel architecture, the Power-On Reset (POR) circuit is essential for ensuring the system starts in a known, stable state when power is applied. Power-on-reset circuit used by the management SoC for power-up behavior so that the circuit input and output can be independently controlled and measured.

------------------------------

#### Inputs and Outputs of the POR Circuit

The Power-On Reset (POR) in Caravel ensures that the design starts in a reset state after power is applied. The inputs and outputs of the POR circuit are as follows:

#### Inputs:
* `vdd3v3:` 3.3V power supply for the core.
* `vdd1v:` 1.8V power supply for the core.
* `vss3v3:` Ground for the 3.3V power domain.
* `vss1v8:` Ground for the 1.8V power domain.

These power inputs are monitored by the POR circuit, which will generate the appropriate reset signals when the power is applied.

------------------------------------------
#### Outputs:
* `porb_h:`  High-voltage (3.3V domain) sense-inverted reset signal . When porb_h is low, it indicates the system is in a reset state.
* `por_l:` Complementary low-voltage (1.8V domain) reset signal. Similar to porb_h, this signal is used to reset components in the 1.8V domain.
* `porb_l:` Complementary low-voltage (1.8V domain) reset signal. Another active low reset signal used for different parts of the low-voltage domain.

These outputs are used to reset various blocks in the system, ensuring that the design initializes in a known state when power is applied.

-------------------

#### Further Reading / References
* https://github.com/efabless/caravel/
* https://github.com/efabless/caravel/blob/main/verilog/rtl/__user_analog_project_wrapper.v
* Sky130 PDK Docs: https://skywater-pdk.readthedocs.io
* https://caravel-user-project-analog.readthedocs.io/en/latest/

