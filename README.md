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
We broke our initial idea into some sub-systems to be expanded on in our design review later, but we know the rough idea is for there to be an array of 8 sensors in three regions (24 in total) through a matrix of AND gates, where each sensor would only be read one at a time and only when the two inputs to their AND gate was powered (obviously). The rough implementation of this strategy is depicted in the image below: <img width="642" height="428" alt="image" src="https://github.com/user-attachments/assets/7d0fbbd6-5dee-4611-b947-832bb9a0fafd" />
We also decided that for maximum comfort and reliable pressure readings, we would use a hard plastic sheet to affix the sensors in place and a soft layer of foam above the sensors to both protect the circuitry and prevent the patient from being poked and prodded. We would also use bluetooth from our MCU to generate the alert to the nursing staff in charge of the patient. My partner made a nice block diagram too but I can't take credit for that, just know that we planned out the subsystems as follows: Power, Alarm, MCU, Sensing, and Analog Acquisition. Power is in charge of housing our Li-Ion battery, charger, and voltage regulator (need 3.3V for MCU and sensors). Alarm would generate the bluetooth signal using either a built-in antenna from our MCU or an external one. Sensing would provide the control signals for the AND gates for each sensor. Analog Acquisition is in charge of wiring the row/column excitation for our matrix of sensors, as well as the op-amp and ADC (external or internal, not decided yet) recommended by the data sheet of the FSR we wanted to use. FSRs, or Force Sensing Resistors, are the part we chose to actually read the pressure inside the pad, datasheet here: https://cdn.sparkfun.com/datasheets/Sensors/ForceFlex/2010-10-26-DataSheet-FSR400-Layout2.pdf. Finally, MCU would tell the sensing subsystem which signals to generate and know which variable to store each reading into to create a map of the sensor readings, then compare it against our set thresholds for how much pressure is too much and how much time is too much time until we genreate an alert. 

# Week 5: 9/21
## What did we do?
We had a discussion on the project details and ironed out our team contract. For the project, we continued brainstorming on how to eliminate ghost currents in our sensor matrix. We decided the best way to stop other sensors from messing up another's reading while still limiting the number of wires we would need to connect to the pad from our PCB was to individually drive each sensors but have the readings come through one main bus instead of individual wires. My teammate had a really nice picture for it but it's not mine so I won't take credit. Basically, we cut down the number of regions from 3 to 2, settling on the Lower Back and Hips since those two were cited as the most prone to pressure related injuries. Then, we would have 16 wires for the positive end (theoretically the positive end, the FSRs are not polarized) of each FSR and one large wire for the reading. Then, by only powering one at a time, we can ensure the reading at each sensor is as accurate as possible. The updated visual aid for this is as follows: <img width="553" height="352" alt="image" src="https://github.com/user-attachments/assets/79ca6c1a-d4dd-4093-873f-00c451ecb788" />

## Team Contract
Being a group of two, making the team contract was pretty easy. Usually in a group of three, one of the members will not be as involved or try to skate by without doing much work. Having two makes this impossible, since any work would likely be done together at the same time. There is not much sense in splitting up when there's only two people's schedule to plan around. While writing the team contract, we said we'd meet up to do all work and only make decisions by complete agreement between us. Any conflict would be resolved with the help of our TA during the weekly meeting. Additionally, we agreed we would both attend every TA meeting and be as honest and prompt as possible when it came to difficulties in any individual work we decided to do later down the line. 

# Week 6: 9/28
## What did we do?
blah
## Design Document
blah

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
