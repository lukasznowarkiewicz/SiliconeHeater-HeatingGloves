  
# SiliconeHeater-HeatingGloves  
  
  
### Motivation  
  
I have always wanted heated gloves for long days on the ski slope. I also enjoy experimenting with technology.  
  
I recently found a new service offered by JLCPCB: custom silicone heaters. There is not much fun in buying off-the-shelf heated gloves, so I wanted to check how hard it would be to design a pair from scratch.  
  
![Image](Attachments/583BF5E7-A0B3-4C0B-BEAF-F21436E20E0B.jpeg)  
  
  
### Design   
  
For the heater design, the goal was simple: follow the JLCPCB flexible heater capabilities listed on order page and prepare the CAD drawings required for them to design a custom heater.  
  
To keep things simple, I selected a few off-the-shelf components:  
  
- [USB-C breakout board with 5.1 kΩ resistors](https://pl.aliexpress.com/item/1005009011843269.html?spm=a2g0o.cart.0.0.7af838daWVdKMu&mp=1&pdp_npi=6%40dis%21PLN%21PLN+8.19%21PLN+8.19%21%21PLN+8.19%21%21%21%40211b441e17756776983078258e7bbc%2112000047573638780%21ct%21PL%211631797217%21%211%210%21&gatewayAdapt=glo2pol) — provides 5 V from a USB-C power source; up to 15 W is possible if the source advertises 3 A.  
![AliExpress](Attachments/23409BB6-5B57-4735-8CE7-B5E364C9F05C.png)  
- [KSD9700 normally closed ceramic thermostat, 40 °C](https://pl.aliexpress.com/item/1005006942683887.html?spm=a2g0o.cart.0.0.7af838daWVdKMu&mp=1&pdp_npi=6%40dis%21PLN%21PLN+18.79%21PLN+18.79%21%21PLN+18.79%21%21%21%40211b441e17756776983078258e7bbc%2112000038883755852%21ct%21PL%211631797217%21%211%210%21&gatewayAdapt=glo2pol) — used as a basic thermal cutoff.  
![Nexpress •](Attachments/1482511C-E328-46B5-844A-0B0BA41E356F.png)  
  
- [704 high-temperature silicone rubber adhesive for electronics](https://pl.aliexpress.com/item/1005009024001203.html?spm=a2g0o.cart.0.0.7af838daWVdKMu&mp=1&pdp_npi=6%40dis%21PLN%21PLN+19.59%21PLN+9.60%21%21PLN+9.60%21%21%21%40211b441e17756776983078258e7bbc%2112000047618156071%21ct%21PL%211631797217%21%211%210%21&gatewayAdapt=glo2pol) — used for insulation, sealing, and mechanical support.  
  
![AliExpress •](Attachments/44FD26E7-FC1B-404F-909B-0EB4F2FA846D.png)  
  
  
### Initial heater design  
  
The heater design started with tracing my own hand with a pen on a sheet of paper. I then scanned the drawing and vectorized it using ChatGPT. This may be a slightly unusual approach, but after a few prompts and clarifications, such as specifying that it had to be a single closed line, it did a good job. I also did not have to open any graphics software.  
  
Scan:  
![Screenshot 2026-05-14 at 21.55.53.png](Attachments/F8F79591-5CCF-49E2-9465-F5490449FEF2.png)  
  
  
Vectorized, closed curve:  
![hand_drawing_continuous_line copy.svg](Attachments/C4AA58E1-67FE-4101-8B0F-671051EBC3D6.svg)  
  
The SVG was then converted to DXF using an online tool.  
  
After that, the DXF was imported into a KiCad project on the Edge.Cuts layer. During the conversion, the imported curves had to be scaled because the SVG did not contain reliable unit information. The correct scale factor was calculated by measuring a reference dimension on the real hand and comparing it with the same dimension in KiCad. The imported outline was then rescaled using this factor.  
  
Comments were added to mark the location of the heating elements, and copper pads were added where the solder contacts for the wires should be located.  
  
![Screenshot 2026-05-16 at 07.31.28.png](Attachments/74C8FB12-BF08-439E-BC54-BED7AC2F25D8.png)  
  
Plotted all layers - saved as DXF   
  
![Screenshot 2026-05-16 at 07.33.49.png](Attachments/9705EB87-0B50-4AB7-90B4-55E3CCB9A830.png)  
  
And sent to JLCPCB  
  
![Tetal Powe](Attachments/D95FEDCC-76DD-4AD9-82CD-F7E78CC93099.png)  
  
### Design on my own  
  
  
After the design was submitted, an email was received saying that the design was too complicated for the automated design tool and that an additional charge would be required for manual design work. Another option was to prepare the heater pattern manually, based on the provided guide:  
  
[https://jlcpcb.com/blog/flex-heater-design-tutorial-complete-guide](https://jlcpcb.com/blog/flex-heater-design-tutorial-complete-guide)  
  
A spreadsheet was used to calculate the required trace width and trace length for the chosen material.  
  
  
![Screenshot 2026-04-09 at 22.15.13.png](Attachments/B8CEBF9C-6251-4E8F-A747-CC66B6B1B2C3.png)  
  
First, KiCad was used for the heater pattern design. The trace length was adjusted manually, using interactive length tuning to extend the loop until the required total length, and therefore the required resistance, was reached. This resulted in a rather unusual trace shape.  
  
![Screenshot 2026-04-16 at 08.07.43.png](Attachments/349F62BB-9181-4468-8A3F-64A83BE4FF66.png)  
  
After receiving feedback, the design had to be corrected because the trace-to-trace clearance and trace-to-edge clearance requirements were not met. At this point, further design work in KiCad seemed impractical because its trace editing tools are quite limited for this type of layout.  
  
  
### Altium attempt  
  
In Altium Designer, DRC rules were configured first. The finger sections were then routed along the edges, and the remaining traces were adjusted by switching routing modes and creating some of the curves manually.  
  
At this point, the design requirements were changed: the heater power was increased from 5 W to 10 W. To achieve this, the trace length was doubled and the sections were connected in parallel.  
  
  
![operatora proboy](Attachments/A51A6FFD-6023-4B5B-958E-F9FA77534BB2.png)  
![motea, STS SUS3O4](Attachments/2064DDDE-96C2-41B9-A45E-3B054C1B7130.png)  
  
  
The DRC setup was straightforward. With online DRC enabled and the trace routing mode set to HugNPush Obstacles, it was easy to maintain the required clearances.  
  
Two DRC rules had to be configured:  
  
- Copper, or any resistive material, to edge: 3 mm  
- Copper to copper: 1.3 mm  
  
  
### JLCPCB order  
  
A few conversions were required for the export because the software used by JLCPCB could not read anything from the original file after import.  
  
The PCB board file was imported into KiCad, plotted as Gerber, and then converted to DXF using an online tool:  
  
[https://online.reaconverter.com/convert/gbr-to-dwg](https://online.reaconverter.com/convert/gbr-to-dwg)  
  
This was the only working solution found.  
  
  
Some corrections were made by JLCPCB team:  
![Solder al1 the pads](Attachments/85C16750-D8CD-42B0-B46A-D32C46014009.jpeg)  
  
The design was then submitted and accepted.  
  
### Received heaters   
  
Despite very unusual outline - the heaters came out pretty good.   
  
![Image](Attachments/625007B4-2BB1-4941-BC68-F894D3FC8F7A.jpeg)  
  
![Image](Attachments/0EDED97A-0034-4576-A5A9-C0626D6819DF.jpeg)  
  
![Image](Attachments/F909663E-A54F-4E88-825E-D746AB3722A0.jpeg)  
  
![Image](Attachments/75AACDF1-7314-4A30-8CE5-FC82D814770A.jpeg)  
  
### Initial test   
  
The heater was powered from a laboratory bench power supply, with the thermostat connected in series. The measured power was close to the target value of 10 W: 9.6 W.  
  
Heating from 20 °C to 40 °C took about 4 minutes. Unfortunately, the electromechanical thermostat had a large hysteresis of above 20 °C. This makes the heater less safe, as some areas could reach up to 60 °C. This definitely needs to be improved.  
  
Apart from that, the electrical performance was good.  
  
![Image](Attachments/F419375B-BAAC-416D-AABB-0F91F2D0C1D8.jpeg)  
  
!['0- 38,9](Attachments/42FD1AEB-EE02-4F16-BF6B-4412EA67C817.jpeg)  


![gif](Attachments/heatCycle.gif)
  
### USB C powered version  
  
  
The USB-C breakout board was soldered and glued in place. The thermostat was also glued in place, and everything was sealed with silicone.  
  
The heater works with USB-C chargers without any issues and is correctly supplied at 5 V with up to 3 A available. This means it should be possible to connect it to a power bank and hide the power bank in a wrist or sleeve pocket of a winter jacket.  
  
![Image](Attachments/8C3292DA-E9B4-4153-BA74-454C091C0CFE.jpeg)  
  
![30 34,31](Attachments/F42EE355-F500-4AA7-81A4-51871B922170.jpeg)  
  
![Image](Attachments/CE99936E-BDA7-4F8D-ABEC-55F9B8772BBE.jpeg)  
  
  
  
### Conclusions and Future Work  
  
- The electromechanical thermostat has quite large thermal hysteresis. It would be better to replace it with an electronic control circuit.  
- The silicone heater is quite thick and not very flexible, which makes it difficult to wear comfortably inside gloves.  
- Zone heating should be considered to maintain a more uniform temperature across the heater.  
- To fit the hand better, each finger section should have some curvature to increase the contact surface area. This may be achievable by forming the heater at a high temperature.  
- Real-life testing still has to be performed at ambient temperatures below 0 °C, with the heater installed inside gloves. It is possible that 10 W per glove will not be sufficient.  
- Electronic heating control should be considered, for example with a small MCU, PTC sensors for individual zones, PWM control with MOSFETs, and a PID control algorithm.  
- For glove integration, a PCB flex heater would probably be a better choice. It would be thinner, lighter, and more wearable, but also more susceptible to mechanical fatigue.  
  
