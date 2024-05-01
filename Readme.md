# Relay control board for M40 CO2 laser cutter power supply

This repository is a KiCad project for a relay control board that controls power supplies for laser cutters (such as M40) with TTL signals like MKS-DLC32.

# About the M40 Power Supply and MKS-DLC32


For details about the power supply for CO2 laser cutters and the CNC control MKS-DLC32, please refer to the information below.

|Item|Link|
|---|---|
|Laser Power Supply (M40)|[AliExpress](https://ja.aliexpress.com/item/32805183446.html?pdp_npi=4%40pre%21JPY%21￥%2011%2C993%21%21￥%208%2C155%21%2175.00%2157.00%21%402140d3ff17145295176637734ee02b%2164707149625%21sh%21JP%212424227286%21&spm=a2g0o.store_pc_allItems_or_groupList.new_all_items_2007447399652.32805183446&gatewayAdapt=glo2jpn)|
|MKS-DLC32 CNC Controller|[Github](https://github.com/makerbase-mks/MKS-DLC32)<br/>[AliExpress](https://ja.aliexpress.com/item/4000828878233.html?spm=a2g0o.order_list.order_list_main.53.1305585aAJdBHK&gatewayAdapt=glo2jpn)|


# About the circuit board created in this project

Reading the description of the M40 power supply, it says that the laser can be controlled ON/OFF based on the voltage level given to P2-L.

| Terminal | Pin | Description|
|---|-----|---------------------------------------------------------------------|
| P2 |  G   | Ground: The foot must connected with laser machine's enclosure and ground properly.|
| P2 |  P   | Water-Protection Switch|
| P2 |  <span style="color: red;">L</span>   | <span style="color: red;">Switch Laser Control: <br/>High Level (>3V) - Laser OFF; <br/>Low Level (≤0.3V) - Laser On.</span>|
| P2 |  G   | Ground: The foot must connected with laser machine's enclosure and ground properly.|
| P2 |  IN   | 0-5V Analog signal control input, also can use 5V PWM signal to control.|
| P2 |  5V   | Output 5V, Max Current 50mA.|

Based on this, it would seem that connecting the MKS-DLC32's TTL-Signal to P2-L should work, but this method did not succeed.


There is a good product for simply testing the M40, and this was used as a reference for designing this board.

[AliExpress - Power Supply Controller](https://ja.aliexpress.com/item/32944454101.html?spm=a2g0o.order_list.order_list_main.10.4671585aD0iIoW&gatewayAdapt=glo2jpn)

In this product, the laser can be turned ON by connecting P2-P to P2-L.

The short-circuit between P2-P and P2-L can be achieved using a Opto-isolator or MOSFET. In this project, the connection between P2-P and P2-L is switched with the MKS-DLC32's TTL signal using an N-ch MOSFET, the [BSS138](https://www.onsemi.com/pdf/datasheet/bss138-d.pdf).

The connections between the BSS138 and other modules are as follows:

|BSS138|Destination|
|---|---|
|Gate(1)|DLC32-TTL(Laser Control)|
|Source(2)|M40-P2-L / DLC-32-S|
|Drain(3)|M40-P2-P|

# How to Use the Project

Please open LaserControlConnector.kicad_pro in KiCad.
