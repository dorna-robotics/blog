# Additional Axes using a Camera Motor and Rail

<p align="center">
<img src="pictures/Thumbnail.png" width="600" />
</p>


<p align="center">
<a href="https://www.youtube.com/watch?v=5VFXYQXdnUo">Link to Youtube video</a>
</p>
In this document we will showcase the Dorna 2's ability to add multiple degrees of freedom. We will go over the construction and the application of the camera attachment and railing.

## Camera Attachment

### Construction

Down below is all the materials you will need to run your Dorna 2 Robot with a camera attachment.

#### Building the Mount

|Items|Links|
|---|----|
|Three 3D printed parts| [link](https://github.com/dorna-robotics/blog/tree/main/camera/STL%20files) |
|8 x M3 bolts 8mm length, 2 x M3 Hex Nuts, 2 x M3 bolts 20mm length|[link](https://www.amazon.com/Sutemribor-320Pcs-Stainless-Button-Assortment/dp/B07CYNKLT2/ref=sr_1_9?dchild=1&keywords=m3+bolt&qid=1623786985&sr=8-9)|
|1 x 1/4" bolt 3/8" length|[link](https://www.amazon.com/Socket-Stainless-Machine-Threads-RoyceMart/dp/B084NWFJZB/ref=sr_1_14?dchild=1&keywords=1%2F4%2Bin%2Bsocket%2Bhead%2Bbolt%2B3%2F8%2Bin%2Blength&qid=1625591901&sr=8-14&th=1)|
|1 x Gear Strip|[link](https://www.amazon.com/Rubber-Flexible-DP500IIS-DP500III-Adjustable/dp/B078QYL2M8/ref=pd_sbs_3/144-0547124-8837416?pd_rd_w=yNFb3&pf_rd_p=a5925d26-9630-40f3-a011-d858608ac88b&pf_rd_r=APJ3XXDH9RQ9VH2T9MB7&pd_rd_r=be764343-9fef-420b-b88e-008e1de311e6&pd_rd_wg=7bTAI&pd_rd_i=B078QYL2M8&psc=1)|
|1 x Driver and 1 x Stepper Motor and Wires||

<p align="center">
<img src="pictures/construction.jpg" width="600" />
</p>

Start by connecting the stepper motor to the motor-attachment(3D-printed part) by screwing the 4 x M3 bolts 8mm length into the four holes. Connect the gear(3D printed part) to the shaft of the stepper motor and tighten the gear to stop any slipping by screwing the M3 bolt 20mm length with a M3 hex nut. Home the robot before mounting the mount(3D printed part) to the robot. Then attach the mount to the robot with 4 x M3 bolts 8mm length. Attach the camera through the biggest hole on the camera mount using the 1/4" bolt 3/8" length. Orientate the camera so the lens is parallel to the shaft sticking out of the mount and facing towards that direction. Now attach the gearstrip to the camera lens so that the clip of the gearstrip is farthest from the shaft sticking out of the mount. Attach the motor attachment and mesh the gear to the gear strip. Tighten it with a M3 bolt 20mm length and M3 hex nut.

<p align="center">
<img src="pictures/cameramount.jpg" width="600" />
</p>

#### Connecting to the Robot

Using the cables provided from buying the stepper motor from Dorna Robotics. Connect the two wires to the motor, the side with the green tip should attach to the stepper motor driver. The side with the white plastic piece attaches inside the control box for the Dorna 2 Robot. The position chosen with effect the which number axis will be selected for the motion. Wire the enable, pulse, and direction into the driver. Be sure to choose the right wires. This can be easily obtained by putting the white plastic piece into the control box and reading what colors associate to what parameter.

### Application

Go to [lab.dorna.ai](https://lab.dorna.ai) and connect the robot and home it. Go to settings and then go to parameters and choose the correct number of axes. For each additional axes added be sure to count up from 5. In this case specifically choose 6 because we have 1 additional axes. Now you can input for j5 and find the values for the maximum and minimum extremes of j. Camera lens turn to different set angles so it is important to find the extremes. Set one side to 0 and spin the lens to find the maximum degree for j. Now you are able to teach your Dorna 2 to film using [lab.dorna.ai](https://lab.dorna.ai) or Python.
To learn more about the [Python API](https://doc.dorna.ai/docs/api/python/manual/) for those that want to use Python to control the Dorna 2. The additional axes can also be controlled in Python.
## Railing

### Construction

[For the documentation on how to set up your Dorna rail](https://doc.dorna.ai/docs/accs/rail/).

### Application

Add one additional axes in [lab.dorna.ai](https://lab.dorna.ai) settings. For this specific case we now have 7 axes. Now you can operate both the railing and camera. 
