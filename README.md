# M920q 3.5" HDD Mod

The stock M920q SATA connector only provides 5V and Ground because the chassis only supports 2.5" drives. Adding an external 3.5" drive is as simple as getting a SATA extension cable and soldering the 12V wire to the motherboard.

## Extension Cable
Any SATA extension cable should work. I used [Cable Matters 2-Pack SATA 22-Pin (7+15) Power & Data Extension Cable - 20 Inches](https://www.cablematters.com/pc-1034-156-2-pack-sata-22-pin-715-power-data-extension-cable-20-inches.aspx) (also available on Amazon). Most extension cables have 4 power wires: 12V, 5V, and 2 Grounds. If you have a drive that needs 3.3V too, see below.

Make sure you know which wire in the extension is connected to which pins. For the Cable Matters, the order is 12V, Ground, 5V, Ground, starting from the side furthest from the connector "L":
![extension](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/c8739972-1833-4005-b2a7-b10f0cb1b945)

Cut the 12V wire, and make sure you cut it with enough length left to reach the soldering point. You'll want to cut it near the male end that connects to the stock connector, the side shown in the picture.

## 12V Connection Points
The 12V wire on the SATA extension cable can be connected to the positive (+) terminal of C442, J13, or any or all of the pins on Q1124. I used C442 because it had the biggest pad. 
![12V connections](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/7bcbb296-aedb-451a-9e49-463abd49fa6c)

**12V Supply Notes:**  This 12V supply is a switcher directly off the 20V DC input, and it only turns on when the machine is booted. It's rated up to 5.5A, but it's shared with the PCI-e slot. PCI-e can do 5.5A over the connector, and SATA can do 4.5A. That means with an exeptionally high load on both, you could exceed the rated current. Over Current Protection is set to 10A, so be careful. Most likely, though, you won't use more than 1A from a HDD. Also keep in mind that the DisplayPort riser connector (JP48) uses 0.4A from the 12V supply when populated.

## Solder Prep
I routed the wire between the two headers, used some kapton tape to hold it down on the pad, and put some flux on the wire end and pad.
![solder prep](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/fd6e6ff6-594f-4fa7-aba4-fbdfd2cc6e96)

## Soldering
You want to add enough heat and solder to get a nice solid joint, with solder reflowing freely and completely covering the wire. Be careful that you don't apply too much solder and heat though, as you'll end up wicking solder up the wire and melting the insulation like I did.
![soldered](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/34e43cb8-2d4c-4908-a525-2980cf78c15f)

## Finishing the Mod
Connect the stock SATA cable to the motherboard, and the extension to the stock cable. There's enough length on the stock ribbon cable to fit around a PCI-e card, if you have one. You'll need to route the extension cable out the back of the chassis either by removing the PCI-e bracket, or printing one with a cutout.
![finished mod1](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/84a3e0c9-7aa0-4ce1-b73c-165c5fe26696)

![finished mod](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/a0ed0cd4-fec9-4fa2-adf3-4dca5e54f798)

## Bonus: 3.3V
Most drives don't use 3.3V. If you do need it, though, for a drive or otherwise, there is one convenient soldering point: the positive (+) terminal of PC848. For a drive, you will need to make sure your extension cable has a wire for 3.3V, which means it will likely have 5 power wires. Cut the 3.3V in a similar place as the 12V wire, and solder it to the pad. 
Be careful, though, because as of [SATA 3.3](https://en.wikipedia.org/wiki/SATA#SATA_revision_3.3), a change in the power connector pinout means that Pin 3 is now Power Disable, and if your drives supports this feature, but you put a constant 3.3V on it, the drive will never start up.

![3 3V connection](https://github.com/kaysond/m920q-3.5in-drive-mod/assets/1147328/c567f250-70cb-4a06-b03c-b01f6a171c9b)

**3.3V Supply Notes:** The 3.3V supply is also a switcher directly off the 20V DC input, and it only turns on when the machine is booted. The supply itself is rated up to 14A, but it's also used for the CPU VCCIO, and this particular connection is only rated up to 7A. It also has an LDO for a 1.8V supply rated up to 0.5A. Keep these in mind when drawing high power.
