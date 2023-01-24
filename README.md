# InSecTT_WSN_Power_Consumption_Dataset

This dataset consists of power consumption measurements of four different Wireless Sensor Network (WSN) protocols. We consider BLE, Thread, the EPhESOS protocol, and UWB in this dataset.


This dataset is a work from [Silicon Austria Labs GmbH](https://silicon-austria-labs.com/) (SAL),  the [Linz Center of Mechatronics](https://www.lcm.at/) (LCM),  and the [Institute for Communications Engineering and RF-Systems](https://www.jku.at/en/institute-for-communications-engineering-and-rf-systems/)  (NTHFS) of the Johannes Kepler University (JKU) in Linz for the [InSecTT project](https://www.insectt.eu/).

# Dataset

## Measurement Setup

In our measurement setup, we use the NRF52840 transceiver [2], specifically, the corresponding development kit of Nordic Semiconductors. Since the NRF52840 supports multiple wireless protocols, we can cover all proposed network protocols but the UWB scenario. For this, we use the same hardware as described in [3] which combines the NRF52832 with the Qorvo DW1000 UWB transceiver unit. We assume that the power consumption in low-power sleep mode of both boards are comparable and differences in the measurements are due to the additional UWB transceiver unit and different network protocols. To make the individual measurements comparable, no acknowledgements or retransmissions are considered in the evaluations.

For the energy consumption measurements, we use the Power Profiler Kit II developed by Nordic Semiconductor. It is a low-cost solution for power profiling, which achieves a considerable measurement resolution of down to 0.2~µA and a sampling speed of 100 kS/s. The Power Profiler Kit is used in source mode to simultaneously power the device and measure the power consumption.

## Configuration of the Different Wireless Network Protocols

### Bluetooth Low Energy (BLE)
As BLE network stack, we use the implementation of the NRF Connect SDK [4] and adapted the provided example programs.
We concentrate on the Peripheral device since it allows more energy saving features compared to the central. 
Here we choose a connection interval of 45~ms and allowed the device to skip up to 40 connection events if no data is available.

### OpenThread
As OpenThread network stack, we use the implementation of the NRF Connect SDK [4] and adapted the provided example programs.
For OpenThread we implemented a Sleepy End Device which can transmit data anytime and periodically polls its parent node with a configured interval of 1~s. 

### Ephesos
For the measurement we use the 1M BLE PHY layer combined with the implementation as described in [5].

### UWB
For UWB we simply transmit periodic beacons to the anchor nodes for localisation. Here we performed our measurements with a centre frequency of 4.5 GHz and a bandwidth of 499.2 MHz. We choose a PRF of 64 MHz and 64 preamble symbols.



## Structure of the Dataset



## Loading the Dataset
The measurements are provided as a CSV file which allows opening the data in various programming languages and programs. Since the individual measurements are relatively large the csv files are compressed with zip. For Python we shall give a small code example to open the sniffer measurement with Pandas where we can directly handle the zip compression:


```python
#import needed packages
import pandas as pd

protocol = "BLE"

# Load the metadata of the dataset
data = pd.read_csv(f"{protocol}.zip", compression='zip')
data = data.set_index("timestamp")

```

For other programms it is recomended to first unzip the measurements and then import it.

# Contact
If you have any comments, questions or feedback please contact
- Julian Karoliny: julian.karoliny@silicon-austria.com

# License 
This dataset is distributed under the [Creative Commons Attributions License 4.0 (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/).


# Acknowledgement
This work is funded by the InSecTT project (https://www.insectt.eu/). InSecTT has received funding from the ECSEL Joint Undertaking (JU) under grant agreement No 876038. The JU receives support from the European Union’s Horizon 2020 research and innovation programme and Austria, Sweden, Spain, Italy, France, Portugal, Ireland, Finland, Slovenia, Poland, Netherlands, Turkey. The document reflects only the author’s view and the Commission is not responsible for any use that may be made of the information it contains.

# Literature

[1] Zephyr Project, https://github.com/zephyrproject-rtos/zephyr, 2022, Version 2.7. <br/>
[2] Nordic Semiconductor, NRF52840 Product Specification v1.1, Feb. 2019.<br/>
[3] L. B. Hörmann, T. Hölzl, C. Kastl, P. Priller, H.-P. Bernhard, P. Peterseil, and A. Springer, “Evaluation of solar-based energy harvesting for indoor iot applications,” in European Test and Telemetry Conference (ettc2022), 2022, pp. 190–198.<br/>
[4] Nordic Semiconductor,nRF Connect SDK v2.0.2,” https://github.com/nrfconnect/sdk-nrf, 2023.<br/>
[5] H. P. Bernhard, A. Springer, A. Berger, and P. Priller, “Life cycle of wireless sensor nodes in industrial environments,”IEEE International Workshop on Factory Communication Systems - Proceedings, WFCS, 7 2017