
PHY:<br>
PHY is a standard module in IEEE802.3. STA(station management entity, MAC or CPU) control PHY by SMI(Serial Manage Interface). IEEE802.3 defines the feature of PHY register with 0~15. Chip manufacture defines address 16-31.

![GitHub Logo](/images/NetCable.jpg)
Most PHYs have auto MDI-X feature, so stright or cross cable are all OK for application.

[Hardware Design](https://www.pianshen.com/article/6827360824/)

RGMII
TXC/RXC 1.5-2ns延迟
修改PCB设计（例如：使用专门设计的蛇形）
