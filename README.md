# Senior Design Lab Notebook
This is my lab notebook, updated throughout the semester with my progress on the Pressure Sensing Pad.

# Week 1: 8/24
I went to the first lecture and did my best to pay attention to the entire 2 hour lecture. 
## Initial Web Board Post
I also made initial web board post with my preliminary project idea. My idea was for a security device that would use microphones arranged in a grid and compare the time of arrival for a given sound to each microphone to determine which direction the noise originated. It would then drive some motors to swivel a camera in that direction and begin recording. This would be a cheap alternative to installing multiple security cameras at all different angles of one's home and deter/record crimes in progress. I wasn't exactly married to the idea but I thought it's better than nothing and feasible for a semester-long project.

# Week 2: 8/31
I went to the second lecture, the lectures in this class are very odd. I also learned that we would only have 4 lectures, which means my tuesdays are looking a lot more free than I thought they'd be! 
## Laboratory Safety Training
I did the lab safety training so that I could have unrestricted 24/7 access to 2070 and the tools within. It was easy.
## Early Project Approval
I met two guys in lecture and agreed to join their group. We were still in the midst of introducing ourselves and deciding whose project to pursue by the time the early project approval deadline came and went, so we didn't submit anything for it. The three of us decided to focus on Rayan's idea of a pressure sensing pad for bedridden hospital patients. It would detect when someone is laying in the same spot for too long and alert someone to come and move them, that way they don't get bed sores or any other pressure related injuries. 

# Week 3: 9/7
We had another lecture this week, mostly about the guest speakers and their projects. Our third group member left us and so it is just me and Rayan now. Rayan was interested in joining Stride Secure sso we wrote up an application to join that project but they never got back to us until they had already selected another group. Quite unprofessional in my opinion. Anyway, we had prepared our own request for project approval anyway so we submitted that. I also had the CAD Assignment due so I worked on that.
## Project Approval
The problem we were focused on solving was to prevent pressure-related injuries in bedridden patients. Evidence cited in our actual proposal points to frequent repositioning as the best way to prevent ulcers from being formed, so we wanted to create a pad that could detect when someone was laying in the same spot for too long and alert a caregiver to come and move the patient via Bluetooth. 
## CAD Assignment
This was a solo assignment, I followed the assignment tutorial to use KiCAD and design a motor driver circuit, complete with USB connectivity, I/O pins, and an MCU. The assignment failed to mention that you cannot use the newest version of KiCAD or else it wouldn't work, so I had to downgrade it after the fact and wasted a good amount of time. It's chill though.

# Week 4: 9/14
## What did we do?
The primary time sink this week was the soldering assignment, we could not get our board's MCU to function properly to save our lives. There was always a short no matter how many times we applied the paste through the stencil and baked it, it took many hours but we got it eventually. We also sat down together and finished the project proposal rather quickly. We already knew what we wanted from the request for approval so this was no challenge for us. 
## Soldering Assignment
This assignment had us take the default PCB from the course staff and affix all of the components on it using the provided stencil and solder paste. The MCU's pins were very small and proved difficult for us but we managed after 8 or so hours. Then, we used the ST-link to flash some given C code and monitored the output in the serial monitor. We demo'd to our TA and went home happy. 
## Project Proposal
We broke our initial idea into some sub-systems to be expanded on in our design review later, but we know the rough idea is for there to be an array of 8 sensors in three regions (24 in total) through a matrix of AND gates, where each sensor would only be read one at a time and only when the two inputs to their AND gate was powered (obviously). The rough implementation of this strategy is depicted in the image below:
<img width="642" height="428" alt="image" src="https://github.com/user-attachments/assets/7d0fbbd6-5dee-4611-b947-832bb9a0fafd" />
We also decided that for maximum comfort and reliable pressure readings, we would use a hard plastic sheet to affix the sensors in place and a soft layer of foam above the sensors to both protect the circuitry and prevent the patient from being poked and prodded. We would also use bluetooth from our MCU to generate the alert to the nursing staff in charge of the patient. My partner made a nice block diagram too but I can't take credit for that, just know that we planned out the subsystems as follows: Power, Alarm, MCU, Sensing, and Analog Acquisition. Power is in charge of housing our Li-Ion battery, charger, and voltage regulator (need 3.3V for MCU and sensors). Alarm would generate the bluetooth signal using either a built-in antenna from our MCU or an external one. Sensing would provide the control signals for the AND gates for each sensor. Analog Acquisition is in charge of wiring the row/column excitation for our matrix of sensors, as well as the op-amp and ADC (external or internal, not decided yet) recommended by the data sheet of the FSR we wanted to use. FSRs, or Force Sensing Resistors, are the part we chose to actually read the pressure inside the pad, datasheet here: https://cdn.sparkfun.com/datasheets/Sensors/ForceFlex/2010-10-26-DataSheet-FSR400-Layout2.pdf. Finally, MCU would tell the sensing subsystem which signals to generate and know which variable to store each reading into to create a map of the sensor readings, then compare it against our set thresholds for how much pressure is too much and how much time is too much time until we genreate an alert. 

# Week 5: 9/21
## What did we do?
We had a discussion on the project details and ironed out our team contract. For the project, we continued brainstorming on how to eliminate ghost currents in our sensor matrix. We decided the best way to stop other sensors from messing up another's reading while still limiting the number of wires we would need to connect to the pad from our PCB was to individually drive each sensors but have the readings come through one main bus instead of individual wires. My teammate had a really nice picture for it but it's not mine so I won't take credit. Basically, we cut down the number of regions from 3 to 2, settling on the Lower Back and Hips since those two were cited as the most prone to pressure related injuries. Then, we would have 16 wires for the positive end (theoretically the positive end, the FSRs are not polarized) of each FSR and one large wire for the reading. Then, by only powering one at a time, we can ensure the reading at each sensor is as accurate as possible. The updated visual aid for this is as follows:
<img width="553" height="352" alt="image" src="https://github.com/user-attachments/assets/79ca6c1a-d4dd-4093-873f-00c451ecb788" />

## Team Contract
Being a group of two, making the team contract was pretty easy. Usually in a group of three, one of the members will not be as involved or try to skate by without doing much work. Having two makes this impossible, since any work would likely be done together at the same time. There is not much sense in splitting up when there's only two people's schedule to plan around. While writing the team contract, we said we'd meet up to do all work and only make decisions by complete agreement between us. Any conflict would be resolved with the help of our TA during the weekly meeting. Additionally, we agreed we would both attend every TA meeting and be as honest and prompt as possible when it came to difficulties in any individual work we decided to do later down the line. 

# Week 6: 9/28
## What did we do?
This week was all about the design document and prepping for the design review. That was about it.
## Design Document
We sat in lab and created the entire design document together. The division of labor was split as follows: I took the problem, solution, visual aid, high-level requirements, physical design, cost analysis, schedule, ethics, and citations, while Rayan took on the tolerance analysis, block diagram, and the functional overview/requirements of each block in the diagram. I thought this was fair, since we had previously discussed all of the information to be put in the block diagram and corresponding explanation but would still take a while to write out, while my parts aren't as technically extensive but much more time consuming to outline. I already put the visual aid in last week's update since we used the same one, but I also made a diagram of the FSR itself as well as the physical dimensions we planned to follow to create the physical pad: 
<img width="512" height="225" alt="image" src="https://github.com/user-attachments/assets/b2117a5f-93c4-4fb6-825a-78e70f476ce0" />
<img width="767" height="322" alt="image" src="https://github.com/user-attachments/assets/cd134722-96c0-4ae0-b474-59ad4a380aa4" />
We decided to use the FSR400 short-tail since the other versions were more expensive without any discernible benefit for our design. We planned on sticking them under a pad, so the exact connection-type didn't matter to us. Short-tail just means the pins are smaller, fine for us. As for the pad dimensions, we googled the average human's back width and the distance between the hips and lower-back and sized the pad accordingly. It would be great to be able to fit the pad to each patient separately, but that would make the wiring much more difficult, so we accepted that we wouldn't be able to do that. Each layer is sized to be a bit larger than the one below it, that way we make sure we dont crush any of the sensors or wiring without any weight being on it. False positives would make our project completely useless, so we must give some slack to make sure we don't trigger alerts in an idle position. Then, I shifted my focus to the cost section, and started finding some links for our components we expected to order. Most of the components were copied from the PCB assignment earlier in the semester, since we planned on reusing the USB, Power, and MCU subsystems, just with swapping the MCU for an ESP32-WROOM-32E for the built-in Bluetooth functionality. The rest was guessed by me, as we knew we would need our 16 FSRs, some analog demuxers for selecting those resistors, an op-amp and 10k ohm resistor for the FSR reading pipeline, and some peripheral resistors for the pull-up and pull-downs needed for the demuxers. All planned parts are listed below:

- 0.1uF capacitors, 8x, $0.77 : https://www.digikey.com/en/products/detail/kemet/C0603C104K5RACTU/1465594 
- 10pF capacitors, 2x, $0.58 : https://www.digikey.com/en/products/detail/yageo/CC1206JRNPOABN100/5884486
- Red SMD LEDS, 5x, $2.00 : https://www.digikey.com/en/products/detail/visual-communications-company-vcc/LSM0805412V/10229621
- Ferrite bead, 1x, $0.12 : https://www.digikey.com/en/products/detail/bourns-inc/MH2029-300T/21556203
- 330 ohm SMD resistors, 4x, $0.51 : https://www.digikey.com/en/products/detail/yageo/RT0805DRD07330RL/1078084
- 1k ohm SMD resistors, 1x, $1.15 : https://www.digikey.com/en/products/detail/vishay-dale-thin-film/PNM0805E1001BST5/2120327
- 5.11k ohm SMD resistors, 2x, $0.21 : https://www.digikey.com/en/products/detail/yageo/RT0805FRE075K11L/1079333
- 33k ohm SMD resistors, 1x, $0.10 : https://www.digikey.com/en/products/detail/yageo/RC0805FR-1033KL/14286524?
- 500 ohm SMD resistors, 1x, $3.42 : https://www.digikey.com/en/products/detail/vishay-dale-thin-film/PLT0805Z5000AST5/2120356
- 1.5k ohm SMD resistors, 1x, $0.10 : https://www.digikey.com/en/products/detail/yageo/RT0805DRE071K5L/1078507
- 82k ohm SMD resistors, 1x, $0.10 : https://www.digikey.com/en/products/detail/yageo/RT0805FRE0782KL/1079415
- 3.3V voltage regualtor IC, 1x, $0.17 : https://www.digikey.com/en/products/detail/texas-instruments/TLV73333PDBVR/5022378
- ESP32-WROOM-32E IC, 1x, $4.99 : https://www.digikey.com/en/products/detail/espressif-systems/ESP32-WROOM-32E-N4/11613125?
- USB-C receptacle, 1x, $1.36 : https://www.digikey.com/en/products/detail/gct/USB4081-03-A/18187473
- 3.7 V Li-Ion Battery, 1x, $5.49 : https://www.digikey.com/en/products/detail/us-electronics-inc/USE-702528-500PCBJST/15781479?
- Li-Ion charger IC, 1x, $4.70 : https://www.analog.com/en/products/ltc1730.html
- Through-hole connection headers, 20x, $3.80 : https://www.digikey.com/en/products/detail/amphenol-icc-fci-/10129378-902002BLF/7915925?
- Tactile SMD switches, 2x, $0.32 : https://www.digikey.com/en/products/detail/e-switch/TL1105AF160Q/80826?
- Crystal oscillator, 1x, $0.72 : https://www.digikey.com/en/products/detail/vishay-dale/XT3518HJRGX12M00E/26472754?
- 8:1 Demux IC, 2x, $1.16 : https://www.digikey.com/en/products/detail/texas-instruments/TMUX1308PWR/13237254
- 10k ohm SMD resistors, 1x, $0.10 : https://www.digikey.com/en/products/detail/yageo/RC0805FR-0710KL/727535
- Op-Amp IC, 1x, $1.22 : https://www.digikey.com/en/products/detail/texas-instruments/LM741CN-NOPB/6322
- Wire kit, 1x, $13.00 : https://www.digikey.com/en/products/detail/busboard-prototype-systems/KIT-ZW-10X3/19200378?
- FSR400 short-tail, 16x, $98.32 : https://www.amazon.com/MECCANIXITY-Pressure-FSR-400-ST-Industrial-Instruments/dp/B0FWH9MP63/ref=sr_1_37?dib=eyJ2IjoiMSJ9.ufWrEaPTt_XMaisLLBzTNgw6h2bhOqjpK3JHuIH6BSlvSICIja5rTZDsKUf8UAPflxLSUx2sgxsKOv7oVIoHxaZUjMd3nP_sqHrMXukRf2r5owerLAz6OrgaHvc-uDtGakJwI9HKUo_EtnlRoNZJP63GVJeamvHHiUgzuwliPiDm6zdP9yXLufV0M_O-ah8EtujBos8iCKVGpTUsiWFVt6ipdrRrA9CgL4lvZpOiE0s.HfHtvwnuJs80eGpHIVQkeY7lH9TshQqtDTsW7RcNRBg&dib_tag=se&keywords=fsr%2Bsensor&qid=1790546173&sr=8-37&th=1
- Stapler, 1x, $9.59 : https://www.amazon.com/Amazon-Basics-Stapler-Capacity-Non-Slip/dp/B079ZV4V3C/ref=sr_1_1_ffob_sspa?crid=H4S0EAI8Q629&dib=eyJ2IjoiMSJ9.rBt9AwBmOqmpBoCpjYvRqDq_M3Sh2qV0bnGbW0v-zAkD71XM_1fyX6Hg-Vm7QbOzTrT9OPwzPg9rel7IftbcS3n1sTZwSUBPMK9U2QgKFXer91YIf5EfAr6nwVk6KyqZDdF1Dw5BMELO__epnqcBJiUzV8uaXvUbksv9P6rMhvq8o7AEaaa64Nm9krgtgnpcTKOESisb7qWduLFfaLpxZGYNexsMTuwur7QPjf5k8tDdS6yM2XKzguNajVaUT-9o9vzY_wDcZLA9g2eFIgi8l4Wn-SEqWOokzhkLc2wnVdE.xQLr_c0tpNE_omDnWtUeATl8VVdFe-oAx9IadoAr0to&dib_tag=se&keywords=stapler%2Bwith%2Bstaples&qid=1790985623&sprefix=stapler%2Bwith%2Bstaple%2Caps%2C168&sr=8-1-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1
- Plexiglass sheets, 1x, $4.99 : https://www.amazon.com/gp/aw/d/B09Y2ZGRRB?pd_rd_plhdr=t&hsa_cr_id=0&qid=1790985678&sr=1-1-5a5562f9-fdfd-4101-9f9d-d76aa9998432&i=aps&aref=L3nrTOT7Js&_encoding=UTF8&ref_=sbx__sbtcd2_asin_0_title&pf_rd_p=90f77631-9599-4fe0-95f8-a40adfe1c762&pf_rd_r=7462MAJ8570NE1GVMZRX&pd_rd_wg=VtQ07&pd_rd_w=I4UbP&content-id=amzn1.sym.90f77631-9599-4fe0-95f8-a40adfe1c762%3Aamzn1.sym.90f77631-9599-4fe0-95f8-a40adfe1c762&pd_rd_r=27bdbff5-853e-4fdf-8a16-c9e0a09b4ca6&th=1
- Foam padding, 1x, $14.99 : https://www.amazon.com/Polyurethane-Cuttable-Furniture-Automotive-Packaging/dp/B0G1HBTDFS/ref=sr_1_2_sspa?crid=2G8WNGXHPZGYA&dib=eyJ2IjoiMSJ9.FvdZOvtmwHjPUMifYhnr6UCkW05_xNkiaVzsCQn9zFc6jKbY6HoeWhpg_vN3iAG4DMKNPcJYSvsum0SlUcNuMpAV6SRvu-yGtXZWwJLICND6p8xdyZmmRtazEtVUzMOijPEgGtp3mcXFohIACj17OohfS2Qz1dMtNgHE_3ftRgUavG7ffNZkGUrVdGiXaH28QHraGGyrAyLmPNgWlyA9RQzpPpi_j4Y-7unstRrgiG--upNYD2mHohS6-NqfEHMV5ysrcGgou37lXSeUMTcB5dg430-8wEPvRHTFhN_jmB8.ZzTwx1LVb1WE3dSWlAT7eaNJ-h4Ddh1pRlkKFazsMdQ&dib_tag=se&keywords=foam&qid=1790985923&s=industrial&sprefix=foam%2Cindustrial%2C131&sr=1-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1
- Pillow cases, 1x, $8.99 : https://www.amazon.com/Bedsure-Grey-Pillowcase-Set-Microfiber/dp/B07PJ4YCL4/ref=sr_1_2_sspa?channelId=500&clpRedir=Y&dib=eyJ2IjoiMSJ9.hxZSSh6F69dAWsrSXyh3KRGZwzjUI2WMDNQ6U1tROVfV-055EW5iC7A1N1iuSfC7NJE4Nf7nhcC9gasGCAJzm8rPPLSyqJzQRRVBmsBwEvI1oaaMiKDkv-mzlTXfkM8z91AbKSBrJVSjsfcoP4HKYd_rQazYXmQfWSpuXMJRjeqOG5oq6xoaD3DNLHhFSjGlVYNop9xJc1GOmUXqnPVrTJAciAngV7zQEPhGEHqO5bWvLwJVeH4Yezkd9x0D59sjRUrKkftE3nvUw71CodibxKjqcdS3MQeRN7F4mO3WInM.nUO71TGpFNlP6AHJcy_KsUcAsRcHrjwmoMP0tbKofjE&dib_tag=se&keywords=pillowcases&plpRedirect=mhFallback&qid=1790986167&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1

# Week 7: 10/5
## What did we do?
blah
## Design Review
blah
## 2nd Round PCB Order
blah

# Week 8: 10/12
## What did we do?
blah
## Breadboard Demo
blah
## Teamwork Evaluation 1
blah
## 3rd Round PCB Order
blah

# Week 9: 10/19
## What did we do?
blah

# Week 10: 10/26
## What did we do?
blah

# Week 11: 11/2
## What did we do?
blah
## Progress Demo
blah
## Individual Progress Report
blah

# Week 12: 11/9
## What did we do?
blah
## Team Contract Assessment
blah

# Week 13: 11/16
## What did we do?
blah
## Mock Demo
blah

# Week 14: 11/23
Thanksgiving break! I worked on the slides for the mock presentation since we are scheduled to give them the monday we get back from break. 

# Week 15: 11/30
## What did we do?
blah

# Week 16: 12/7
## What did we do?
blah
