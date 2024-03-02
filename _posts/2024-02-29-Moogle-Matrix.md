\MMogPad

> Disclaimer: I am new to doing write-ups of projects so please let me know if there is any information you would like to know that I have not included here- Let me know!   

This project started as a response to seeing the HorixFFXIV game-pad collaboration. It seemed like an interesting concept but there were a few things I didn't like. 

 1. The 'ergonomic' design: I'm sure that for many people this design is really nice for their hands. For me though- the design feels terrible. and if I'm honest I don't need so many buttons. 
 2. Price:  I am NOT paying 140$ for an oversized macro-pad with joystick. 
 3. Aesthetic: it is very 'gamer'-y and to be honest I don't find that to be very appealing- that said it is also HUGE. I don't want most of my limited desk space to be taken up by some ugly giant macropad. 
 4. Its not pink. 
So the first thing i needed was a Macro-pad. For this i got a dumbpad by Keedb. Originally I had gotten six kits to make some for myself and friends as holiday gifts. 
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20231230_195903.jpg)
This was  by far the easiest part of the project. Instructions for the macro-pad are simple enough to find online.  You simply sodler the arduino pro micro to the board, then you solder the screen to the board. In order to keep components isolated I added Kapton tape to the back of the OLED. While i doubt it would realistically cause a short- Rather be safe than sorry.

The next thing to do was just to flash the firmware. I was able to customise the macropad for each person. (i had to lube switched for each person, never again)
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20231231_171528.jpg)

Once I decided to add a joystick to one I first had to figure out WHERE. I took the time to look at the schematic and try to figure out what pins were available. 
The scematic pointed to the encoders:
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/pic.jpg)

The joystick pins are as follows :gnd, x, y , 5v 

I connected the 5v and gnd, and then connected X and Y to the encoder pins. 
![aww yeah such amazing wiring](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20240222_160001.jpg "aww yeah such amazing wiring")

I had used QMK to flash the firmware onto the macropads. The change to add a joystick was deceptively simple: 
I added the joystick enable to rules.mk
`JOYSTICK_ENABLE = yes`

Then I created a config.h file  and  the joystick info: 
`// Min 0, max 32`
`#define JOYSTICK_BUTTON_COUNT 0`
`// Min 0, max 6: X, Y, Z, Rx, Ry, Rz`
`#define JOYSTICK_AXIS_COUNT 2`

Then I added the configuraiton for the joystick:
`joystick_config_t joystick_axes[JOYSTICK_AXIS_COUNT] = {`   
   ` JOYSTICK_AXIS_IN(B4, 150, 400, 800),//y`
   ` JOYSTICK_AXIS_IN(B5, 750, 520, 150), //x`   
`};`

The three numbers after the pins are the resistance values.  The joystick I used was (originally) a psp joystick, later changed to a 3ds XL one. 
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20240301_203617.jpg) 

The copper pins in the joystick drag accross the traces on the PCB and they vary the resistance coming out of the x,y pins. To figure out these numbers we need to figure out the resistance being goign intot he analof pins. We can use the ability to print values to serial and have it print out the reported values. This cna give us and average Max, average Min, and the average reisstance at rest. 

Swapping the Max and Min can help us change the orientation of the joystick, swapping up and down, and left and right. 

Once all fo this was settled and written onto the firmware we could begin testing and design a case.

I am NOT good at case design. In fact- I suck. But by golly did I do my Best. ![This is what I had to work with](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20240221_193110.jpg)

I designed a few iterations- first i taped the joystick on jsut to get a feel for where my hand fell on the board. Thsi was  pretyy 'eclectic' process. I just felt around, tryignt o see wher ei would enjoy it most. I quickly realized that I would need to have some kind of wrist rest to stabilize it as I moved the joystick.  

Iterated througha few designs using some filament colros I didnt like: 
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20240227_100857.jpg)

Eventually al ovely friend suggested I separate it into modular pieces and I didn just that, meaning i could remove the wrist rest and hide the bulk when I wasnt playing! 

Heres some pics of the compelted project: 
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20240228_080845.jpg)
![](https://raw.githubusercontent.com/MommiDearest/Keyboard-Diary/main/images/MMogpad/pictures/20240228_081307.jpg)

Anyway- That is all for this project, let me know if you feedback or questions! You can send any questions you might have [here](mailto:celes.meh@gmial.com "here")!!



