# Tracing an Image

In this document we will show how you can use the dorna 2 robot to trace an image in svg format. We will explain the concepts and show how you can modify the code to your preferences.
## Toolhead Installation
### Parts
We will need to attach the pen holder toolhead. We have the link to the materials below. You can use a 3d printer for 2 of the parts and will need to order a few of the materials. Use the default settings when 3D printing and print with a raft. We will need 9 M3 ½ inch length screws, 1 M3 bolt, 2 3D printed parts, 2 springs, 1 pen(preferably BIC Pen),  and 2 50mm Standoff Column Spacers with 5mm outer diameter. Show picture of all parts
### Construction
Put the small 3D printed piece around the shafts and the springs attached as well. Make sure to have the small 3d printed piece oriented to hug the wall farthest from the mount holes on the large 3d printed piece as shown below. Screw 4 M3 screws into the ends of the shafts to lock them in. Now attach the part to the Dorna 2 robot by using 4 M3 screws. Lastly put the pen through the large hole and screw on an M3 bolt and nut. If the pen is too small for the hole. An easy solution can be to wrap it in tape to create a bigger outer diameter.
## Code
### Image
Find an image in SVG format or a file that can be edited in svg format. You can read into how the svg format works thanks to [MDN](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths).
### Actions Needed to Run
The line below allows you to connect to your dorna.  
```python
robot.connect("ip address", 443)
```
This function allows you to pick your image.
```python
cmds = svg(10).gen('filename.svg', x_max, y_max, x_min, y_min, a, b, cp)
```
Make sure it is in the same directory as your code on your computer.Next you will set the width and length of the image you want in mm.
```python
#set the x_max and y_max
    x_max = 1
    x_min = 0
    y_max = 1
    y_min = 0
```
When the program is run. It will ask you to turn off the motors. Then a command will ask you to direct your robot to the left bottom corner of your paper. The command will then ask you to direct the robot to the top right of the paper. Lastly you will then direct the robot to a point along the line clockwise of the left bottom coordinate. A picture shown below.![Setting Points](C:\Users\Joseph\Documents\LatestDorna\dorna2-python-master\example\SetupPicture"Setting Points")

## Explanation of Code
### Main Function
We can take a look at the main function. The main function starts by connecting to the robot and setting the paper to the right parameters.
```python
if __name__ == '__main__':

    robot = dorna()
    print("connecting")
    robot.connect("ip address", 443)
    wait_id = 100
    print("done connecting")
    # now lets write the same thing  and delete it:
    #set the width and length
    width = 20    
    length = 15

```
Next the starting points are intiliazed by calling a function. With the guidance of the user we can set the 3 points of the paper to understand the size of the paper and to understand the equation of the plane. This is used so if you wanted the plane rotated you could do it.
```python
#intialize the 3 points on the plane,Left Bottom-Point along line-Top Right
    error,LB,M,TR = startingpoints(robot)
    print("LB",LB)
    print("M",M)
    print("TR",TR)
    #check if there is an error from last function called
    if(error == 1):
        print("need to restart")
        robot.close()
```
Next we call a function that allows us to find a 3rd corner of the paper. This helps us define the paper more
```python
#calls function to find 3rd corner for new plane
    TL = findcorner(LB,M,TR)
    print("TL",TL)
```
We want to convert all points on an x y axis to a xyz axis given by the 3 corners. This can be done by a linear formula of
[x,y,z]= T * [x0,y0] + [B]
The T stands for transformation and can be solved for because now we have the 3 corners of the plane. T is a 3x2 matrix. B is a 3x1 matrix. B is how much the position is off initially. 
Next we want to find the perpendicular vector from the plane. This will help to move off the paper to different points.
```python
#perpendicular vector in unit vector form
    cp = perpendicularvector(LB,M,TR)
```
Next is a function that creates the path. This is the bulk of the code. It will read the letters and numbers and correspond a path to create for the robot.
```python
cmds = svg(10).gen(‘filename.svg', x_max, y_max, x_min, y_min, a, b, cp)
```
The last few lines command the robot and turn it off
```python
for cmd in cmds:
        print("len: ",len(cmd))
        for c in cmd:
            msg = json.dumps(c)
            print(msg)
            robot.play(msg)
        print("wait")
        robot.wait(id=wait_id, stat=2)
        wait_id += 100
    
    robot.close()

```

