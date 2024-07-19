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
- 
