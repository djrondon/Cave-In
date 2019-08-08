# Cave-In
Cave-In arcade game 

Bagman was an arcade machine game from the early 80's, made by the french company Valadon Automation (we recognize any copyright if apply)
where I spent a lot of coins. Now I'm learning Red language, I thought it was a good idea to try to imitate the game, just to learn while having fun.

I know it does not have the quality of the true arcade game, but the goal is not to market it, but to learn, to play and share the code to others, so they can also learn in his way. In addition there are several known failures and others that will discover, so the development continues. I publish it just so that others can try it and have fun as me.

To run it just download the folders tree and click on cave.red file. Have fun!

INSTRUCTIONS FOR CREATING NEW LEVELS:

Levels are made of one folder with two files inside, the scenario image cavern.png, and the 
objects configuration file items.txt. The level name would be the folder name.

First of all we need to create a new folder with his name, better to use the same pattern
of uppercase letter and number, I do prefer to use letter "L" for my own levels, but I 
strongly reccomend to use a different one, as for example "X".

Then we have to amend the (current) line 20 of cave.red file. That line contains the block 
holding the level names as:  Levels: ["L1" "L2" "L3" "L4"]  to 	Levels: ["L1" "L2" "L3" "L4" "X1"]  
for example. I do change this line for the first level to be the one I'm working, so the
line would have this aspect:  Levels: ["X1" "L2" "L3" "L4" "X1"] so you will start the game
at the desired level, then when level is done then restore the line the normal content.

SCENARIO IMAGE:

Then we have to copy the files cavern.png and items.txt from an existing folder, from
that way we will not start from scratch. It is important not to modify the dimensions of
cavern.bmp that contains the scenario of the game, since it would produce unpredictable results
in the game, these dimensions are 1599x600 pixel.

Once this is done, we can begin to modify the appearance of the scenario, I always use
paintbrush & pixelformer, but any bitmaps editor works. It is important to preserve the color
of the terrain and the stairs, since the game is based on that color to stop the effect of
gravity, you may use any color combination and these colors values can be changed in the level
configuration file, items.txt, by using a line that starts with "&" such as: 
& TerrainColor 100.125.150.0 or & StairsColor1 200.200.200.0 and & StairsColor2 150.150.150.0
that way we can change the color of the scenario and dynamically set the value to the game.

The design of the scenario is free hand, you just have to bear in mind that you have to use 
those colors in the areas where objects move, for the subject of gravity. A part of this, is 
very important properly place the stairs, and make sure each upper end of stair have a ceiling 
at the adecuate distance (50 pixels), for the guards to detect end of climbing. It is also 
noticeable not to locate stairs at the side of walls not being external perimeter, so the
guards would be able to turn back and exit dead ends. The kart handles must be placed at the 
point iver the kart stops, the distance is about 45 pixels, but the handle routine will look up
of the boy for 45 pixels to locate the HandleColor value, so it have some flexibility on distance.

You must draw the kart cable and stop terminator marks, the lifters holes and cables (if any) and
use the LifterCable value as color for them, there is an unused function that looks for this color
that may be used in the future, so I recommend to use the same color for kart and lifter cables.


OBJECTS CONFIGURATION FILE:

This is where we locate te objects that appear in the level, including the scenario file.
A line contains this:
ItemType|ObjectName|FaceName|FaceSize|FaceOffset|Rate|Stops|TimeOfTool|Direction|Gravity|ImageFiles
- ItemTypes start with: (A)gent (B)and (C)avern (D)rop (G)oldBags (J)ohnDoe (K)art (L)ifter (P)assage (S)pider (T)ools (W)barrow
- Stops (for lifters (up-down) or karts (left-right) way 0x0,0x0,...) or 0x0 for other types
- Location (Stop #)
- Direction (1 Down/Right -1 Up/Left)
- For (B)and first stop indicates axis displacement 1x0 -> Horizontal  Other value -> Vertical
- (P)assages must be grouped pairs passage1 and passage2, passage3 and passage4 ... (use direction as grouping field)
- For (A)gents first ObjectName & image files letter must be "f" if agent is female so as "fagent3"
- To modify default GameData/word values:  & word value   (value can be tuple! logic! or integer!)

Each comment line starts with "#"
EXAMPLE:

& TerrainColor 89.89.89.0

& StairsColor1 200.191.231

& StairsColor2 63.72.204.0

& DropGravity 1

CAVERN|cavern1|cave|1599x600|0x0|0:0|0x0|0:0|0|0|cavern.png
AGENT1|agent1|age1|22x34|1550x20|0:0:0.04|0x0|0:0|0|1|fagent-l1.png|fagent-r1.png|fagent-l2.png|fagent-r2.png|fagent-l3.png|fagent-r3.png|fagent-s1.png|fagent-s2.png|fagent-s3.png|fagent-s4.png
GOLDBG|gold1|gld1|8x12|75x50|0:0|0x0|0:0|0|1|gold1.png
GOLDBG|gold2|gld2|8x12|75x240|0:0|0x0|0:0|0|1|gold1.png
TPICKAX|pickax1|pkx1|9x10|350x320|0:0|0x0|0:0:10|0|1|pickax1.png
TPICKAX|pickax2|pkx2|9x10|1400x230|0:0|0x0|0:0:10|0|1|pickax1.png
LIFT1|lifter1|lif1|35x10|201x53|0:0:0.0001|201x53,201x185,201x257,201x337,201x417,201x586|0:0|1|0|lifter-1.png
LIFT2|lifter2|lif2|35x10|1205x109|0:0:0.0001|1205x110,1205x235,1205x312|0:0|1|0|lifter-2.png
LIFT3|lifter3|lif3|35x10|1105x312|0:0:0.0001|1105x312,1105x400,1105x585|0:0|1|0|lifter-2.png
LIFT4|lifter4|lif4|35x10|1305x585|0:0:0.0001|1305x312,1305x400,1305x585|0:0|-1|0|lifter-2.png
LIFT5|lifter5|lif5|100x15|1486x582|0:0:0.0001|1486x290,1486x400,1486x582|0:0|-1|0|lifter-3.png
BAND|band1|bnd1|100x1200|750x-600|0:0:0.1|0x1|0:0|1|0|lavafall100.png
PASSAGE1|passage1|pas1|50x40|82x132|0:0:4|0x0|0:0|1|0|passage-G.png
PASSAGE2|passage2|pas2|50x40|1196x55|0:0:4|0x0|0:0|1|0|passage-G.png
PASSAGE3|passage3|pas3|50x40|675x534|0:0:4|0x0|0:0|2|0|passage-G.png
PASSAGE4|passage4|pas4|50x40|873x534|0:0:4|0x0|0:0|2|0|passage-G.png
SPIDER1|spider1|spi1|9x7|510x325|0:0:0.15|0x0|0:0|0|1|spider-l1.png|spider-r1.png|spider-l2.png|spider-r2.png|spider-l3.png|spider-r3.png
SPIDER2|spider2|spi2|9x7|930x190|0:0:0.15|0x0|0:0|0|1|spider-l1.png|spider-r1.png|spider-l2.png|spider-r2.png|spider-l3.png|spider-r3.png
WBARROW|wbarrow1|wba1|26x17|155x550|0:0|0x0|0:0|0|1|barrow-r1.png
JOHN|john|doe|22x34|160x15|0:0|0x0|0:0|0|1|thief-l1.png|thief-r1.png|thief-l2.png|thief-r2.png|thief-l3.png|thief-r3.png|thief-s1.png|thief-s2.png|thief-s3.png|thief-s4.png|thief-bl1.png|thief-br1.png|thief-bl2.png|thief-br2.png|thief-bl3.png|thief-br3.png
