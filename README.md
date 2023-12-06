# Sylvester’s Knowledge

computer 🖥️

[The best website on the whole entire internet](https://bigpierogi.net/)

# **General rules/suggestions for making schematics, PCBs, uploading, and ordering**

Note: **I’m not a expert**, these are just things i’ve learned in my time making PCBs. You should take these as strong recommendations on what to do when you create a PCB and schematic, because I make a lot of PCBs. Feel free to tell me if something is dumb or wrong.

## Must Know Terms

- SMD
    - Surface Mount Device
    - A component that is soldered only onto 1 part of the board, with pads
    - Allows you to route traces/other components under it
- Through Hole
    - A component that goes through all layers of the board
    - Doesn’t allow you to put components/traces under that component
- Schematic
    - A layout of how stuff SHOULD be connected on the board
    - A document in Kicad/Eagle that you create before making the board
- Symbol
    - Refers to a component on a schematic
    - Is connected to other parts on the schematic, could be a chip, resistor, etc.
- Footprint
    - Refers to a component on a board view
    - The shape of the component physically on the board
- Via
    - A hole in a PCB
    - Used to make electrical connections, whether between layers or traces
- Traces
    - The “wires” of a PCB
    - These are used to connect different components together in board view
- Gerber
    - Production files used to manufacture PCBs
- Routing
    - The process of connecting everything on the board

---

## Programs

- You should use KiCad, Not eagle
    - Eagle is kinda poopoo and old
- KiCad 7 is the latest: [https://www.kicad.org/download/](https://www.kicad.org/download/)
    - Compatible with Windows, OSX, and Linux (arch included)
    - Easy to learn, if you previously used Eagle this will be similar
- Altium is also good, but its expensive and for actual engineers only
    - Windows only

---

## **Schematic Wiring**

### **Useful Shortcuts for KiCad Schematic View**

- W
    - Creates a wire
- A
    - Adds a normal Symbol
- P
    - Adds a power Symbol
- L
    - Creates a net label
    - Use CMD/CTRL + L for a global label
- T
    - Creates text
- X
    - Creates a no connection flag
- alt + 1/2
    - Switches between grids
    - Be careful about this, if you switch accidentally, it could mess up the layout of your schematic, and how stuff attaches
- Always check the data sheet if extra things are needed for the part to function properly
    - ex: pull up resistors for a signal pin
- Whenever you have power going into a chip
    - Put a 100nf/.1uF capacitor in front of the power input for the part
    - ex: 5v -| |- GND
    - Helps smooth out the power going into it
- If you find a symbol online, double check that it is the right dimensions and pinout
    - Look at the part data sheet, or measure it yourself if you’re crazy
- Don’t have paths of signals cross each other
    - i.e Don’t have any green lines that don’t need to be connected together cross
    - Will look terrible, and will confuse you later
- Use labels when routing the connections when applicable
    - Will make searching for signals easier, and make it more appealing to the eye
- **USE LABELS ON EVERYTHING**
    - It will be hard to find stuff if you don’t use labels
    - Don’t repeat label names also
- For connections like 5v or GND, use the built in symbols instead of labels
    - Makes it more universal
    - Easier to find the common connections
- Don’t put all your symbols and connections close together
    - Some space is good, but too much will be just as bad

---

## **PCB Layout and Setup**

### Setup your Board first

- File→Board Setup
    - I recommend a 4 layer board
        - Layer 1 and 4 is signal layers, layer 2 and 3 is power plane
        - This creates good grounding and minimizes interferance and noise in signals
    - For a 2 layer
        - Keep them both signal
- Setup your trace and via size
    - Traces: 0.2mm, 0.4mm, 0.5mm, 0.6mm, 0.8mm, 1mm
    - Vias: 0.2mm/0.4mm, 0.3mm/0.6mm, 0.4mm/0.8mm, 0.5mm/1mm
- Create a board shape
- Create a filled copper zone
    - Look at the right toolbar in board view
    - If using 2 layers
        - Select layer 1 and 2, and make the net GND
        - Surround the entire board in a closed rectangle
    - If using 4 layers
        - Select layer 2 and 3, and make the net GND
        - Surround the entire board in a closed rectangle

- Regarding IC’s
    - Place 2 decoupling capacitors if possible
        - Ex: 100nf + 100uF in line
        - Keep them as close as possible to the IC
        - Place the smaller capacitor closer to the supply pin
- Don’t cram the board all together if you can (or if you don’t want to)
    - You don’t want them to close, because routing will be harder
    - Don’t put them all the way across the PCB though, as that will waste space and make traces unnecessarily long
    - Sometimes you want parts to be closer together, for example, decoupling capacitors near chips, or pull up/down resistors.
- If possible, put parts inline with each other that are connected
    - ex: If a chip and resistor are connected to each other, put the resistor inline with the pin on the chip
    - Ensures traces are straight, good practice
- Make sure your parts are on the correct side of the board
    - Don’t put stuff that has to be on the front on the back, and stuff that has to be on the back on the front
- Be mindful of a parts footprint
    - If a part has a large footprint, don’t put anything inside the footprint
    - You can put parts on the other side of the board with the footprint, if there are no pins sticking out of the part
- Roughly layout your parts first
    - Don’t try to align everything from the beginning
    - Align everything to be straight and nice at the end
- Be mindful if a part is SMD or through hole
    - If its SMD, you can put parts on the other side
- If you want to put screw holes onto a PCB
    - Put them on the board first
    - Will affect where the rest of your parts go and how you will route
- If ordering from JLCPCB
    - Added a small text saying “JLCJLCJLC”
        - This will put the order number there

---

## **PCB Routing**

### **Useful Shortcuts for KiCad Board View**

- X
    - Route Tracks
    - While routing, press ‘v’ to add a via for switching layer
- CMD/CTRL + Shift + V
    - Create a free standing via
- CMD/CTRL +Shift + L
    - Creates a line
- CMD/CTRL + Shift + T
    - Creates text
- CMD/CTRL + Shift + M
    - Measure Tool

### Useful Resources

- [For in depth information](https://docs.toradex.com/102492-layout-design-guide.pdf) on routing
- [How to achieve proper grounding](https://www.youtube.com/watch?v=ySuUZEjARPY)

### Trace Sizes

- 0.2mm-0.4mm
    - For signals, since they do not carry much power
- 0.5mm-0.8mm
    - For lower power traces, a couple of amps max at 12v/5v/3.3v
- 1mm+
    - For high power traces, multiple amps/watts
    
- Which via size do I use for each trace?
    - Whichever fits
    
- Route by hand, don’t use a auto router
    - Unless you very properly set it up, it will not route very well, and will not follow good practices
- Try to have the same amount of ground layers as signal layers
    - ex: For 2 layer boards, make 1 layer ground (usually the bottom).
    - For 4 layers, make 2 layers ground (usually the middle 2).
- Try not to route through ground layers if possible
    - May make grounding of the board worse
- When routing, make sure that when entering/exiting a SMD (Surface Mount) pad or vias, you are straight either vertically or horizontally
    - Looks better, and is considered good practice
- Make your power traces thicker than your signal traces
    - These traces will have more power going through them, so they need to be thick or else they could fail
    - Heats up more if their thin
- Don’t route traces right next to each other, try to give them some space in between each other
    - Reduces interference
    - Also put ground vias in-between traces to help with grounding
- Make sure no traces have a sharp angle
    - ex: 90 degree angles
    - Try to do something more like 135 degrees
    - Can make funny issues with connections
- If you want to make a 3 way trace
    - Try to avoid, and instead, do a daisy chain if possible
    - One option is to have it “branch out” 135 degrees each way
        - Like a triangle with 3 lines coming out of it
        - Prevents sharp angles
        - DO NOT USE if you are using a high speed signal, could cause bounce back and issues
    - Another (and probably better) option is to put a via the size of the trace in between
        - This will allow you to branch out straight out of the via, without having to make a weird triangle
        - Currently, I prefer this method
        - Possibly OK for high speed? Don’t take my word for it
- Avoid routing power traces and signal traces together
    - i.e If you have a power trace on layer 1, try to avoid routing a signal trace on layer 2 right on top of it
    - Could cause some interference
    - Should cause minimum issues if the board is 4 layer, and there are 2 ground layers in between (traces on layer 1 and 4, gnd on layer 2 and 3)
- Have someone else look at your routing with you
    - Will be much easier to spot bad routing
    - Lets you have more brains looking at your stuff
- Try not to have silkscreens overlap with SMD pads or Vias
    - Generally bad practice
    - Not super important though
- At the end of routing, put GND vias all over your board
    - Put them where you used vias to route in between layers
    - Also put them between traces
    - Make sure your board has no ungrounded spots, unless told otherwise
- Put silkscreen texts for signal labels and part labels
    - Will make finding certain signals easier
    - Easier to find what parts you have to solder and where
- Export your production files (gerbers) and put them in a zip when ready for production
    - [Guide for gerbers for JLCPCB](https://jlcpcb.com/help/article/362-how-to-generate-gerber-and-drill-files-in-kicad-7)
    - View them in a online gerber viewer to get an idea of how they will look, and to see any possible errors

---

## When uploading to GitHub

- Have a .gitignore
    - Helps reduce unneeded files
- Include a .zip file with the PCB production files (gerbers)
    - Lets you view the board online and print the board
- Cut out any files not needed
    - Only include the project file, schematic, pcb, gerbers, and photos if you want to include those
    - Don’t include backups, or any auto generated files (cache files)
- When uploading to MedShifty GitHub
    - Put “PCB_” before the name of the board when naming a repo
    - Helps identify PCBs easier in the future

---

## When ordering PCBs

- I recommend JLCPCB
    - [Guide for gerbers for JLCPCB](https://jlcpcb.com/help/article/362-how-to-generate-gerber-and-drill-files-in-kicad-7)
    - Usually cheap if the board is under 100mm X 100mm
    - 2 dollars for 5,  2 layer boards
    - 7 dollars for 5, 4 layer boards
    - Shipping can range from 2 weeks to a few days
        - Price of shipping may also vary
    - Chinese company
    - they send you Christmas stickers if you order during the holidays
- OSH Park is also a ok company
    - Not much faster than JLC
    - Have to pay more to make them
    - American company
    - they do not send you Christmas stickers if you order during the holidays

---

## How to get better??????

- ~~you don’t~~
- Play around with the tools and buttons
    - Try out all the buttons and tools on both sides
    - Some will do cool stuff, others are dumb (like switching measurments to inches)
- Practice key binds
    - These will make you more efficient, and work faster
- Practice making PCBs in the software
    - Videos and articles will only get you so far
    - The more you make PCBs and schematics, the more you will learn and the better you will use the software
    - Try new projects or ideas, even if you don’t think you will get them printed
- Look at other PCBs people made
    - See what they did vs. what you do, and if what they do is good practice, try to integrate that into your own boards
    - For example: [**My github**](https://github.com/SonOfCheevap)  has some boards that I have made in my free time that I consider “good.” [**Gold Rush Robotics at UNC Charlotte**](https://github.com/Gold-Rush-Robotics/PCB) also has some good custom PCBs…because I made all of them.
- [Youtube tutorials like this one](https://www.youtube.com/watch?v=b-7bMl6fJio)
    - These are good for starting out, but once again, these will only get you so far

---

# The end goal

![Sudo apt-get in the bin](Sylvester%E2%80%99s%20Knowledge%2057d5770106e34c32a90211a852cee3c9/Untitled.png)

Sudo apt-get in the bin
<!--
**SonOfCheevap/SonOfCheevap** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
