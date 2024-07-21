# Anveshak-main.py-documentation

---

## Class Atrributes:
- `self.is_identified` - bool variable to check if red cylinder detected
- `self.goal_reached` - bool variable to check if close enough to goal linearly
- `self.goal_reached_angular` - bool variable to check if rover is aligned with goal
- `self.p_x,self.p_y` - coordinates of centroid of detected by mask_red function
- `self.cord_x1, self.cord_y1, self.cord_z1` - unused variables
- `self.cv_image` - image from zed2i rgb camera
- `self.image_arrived` - bool variable to check if image from rgb camera arrived
- `self.main_control` - Autonomous task consists of various stages, this shows that the control shifted to cylinder detection 
- `self.depth` - depth of self.p_x,self.p_y from rover(uncorrected)
- `self.cord_x,self.cord_y,self.cord_z` = depth of centroid of object from rover after appyling correction

---

## Variables
- `g` - object of class WheelRPM ROS msg to set velocity 
- `goal_coord` - numpy array of `self.cord_x1, self.cord_y1, self.cord_z1`
- `msg.data[1],msg.data[2],msg.data[0]` - z,y,x coordinates offset taking poisition of zed2i camera into effect
- `d` - distance of centroid from rover using depth coordinates
- `kp` - propprtionality constant

---

## Publishers
* `self.tube_pose_pub`: Not used in code.
* `self.vel_pub`: Publishes `msg` array containing goal_coordinates to arm for IK.
* `self.bool_pub`: Provides boolean value if arm should start IK.
* `self.velocity_pub`: Publishes linear and angular velocities to "motion" topic.

---

## Subscribers:
* `self.image_sub`: Subscribes to zed2i node giving colour image data.
* `self.depth_sub`: Subscribes to zed2i nodes giving depth data.

---

## Class Methods:
* `__init__`: initalises the 4 publisher and 2 subscribers mentioned above. It also initialises a nunmber of class attributes listed above.
* `main_callback`: unused function
* `Depth`: callback function for zed2i depth camera subscriber(`self.depth_sub`). It bridges the depth camera data to cv2 thorugh `cv_depth` and then sets `self.depth` to the
  depth of the coordintaes `self.p_x,self.p_y`(centroid detected by `mask_red` function).
* `show_coordinates`: applies a correction formula on `self.depth` to get the exact x,y,z coordinates of the centroid of the object from rover
* `callback` callback function for rectified image from zed2i camera. It bridges the data to cv2 through `self.cv_image`.
* `tube_frame`: unused function
* `mask_red`: function to detect centroid of red object. It converts the image to hsv and detects contous in the upper and lower hsv values of red used.It then uses cv.moments to
  find the centroid of each object with non zero area and adds them to a list. It however returns only the last value of the centroid found. It also draws a circle and the countours
  although the image is never displayed
* `main`:  
