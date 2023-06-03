[Research Track II](https://corsi.unige.it/en/off.f/2022/ins/60236)<br>
[Hafiz Muizz Ahmed Sethi](https://github.com/notMuizz)<br>
[M.Sc Robotics Engineering](https://corsi.unige.it/corsi/10635)<br>
**Professor:** [Prof. Carmine Tommaso Recchiuto](https://rubrica.unige.it/personale/UkNDWV1r)


## Jupyter Notebook Assignment
Jupyter Notebook is a web application that is open-source and enables the creation and sharing of documents. These documents can contain live code, equations, widgets, animations, visualizations, and explanatory text. The notebook itself is stored in the "Jupyter" folder.

For my assignment in the RT1 course, I developed a user interface using Jupyter Notebook. The main objective was to replace the existing user interface node with an interactive notebook. This notebook provides real-time updates on various aspects such as the robot's position, target locations, closest obstacle distance, and the status of target tracking. To achieve this, I utilized widgets for user interaction and incorporated plots to visualize different elements like the robot's position, the path to target positions, laser scanner data, and the count of reached and unreached targets.

**HOW TO START THE NOTEBOOK**
To begin, navigate to a workspace of your choice or create a new workspace. Inside the workspace, access the "src" folder. From there, clone the repository that includes two packages: the package provided by the professor named **assignment_2_2022**, which contains the necessary launch file for initializing everything, and the package you have personally created called **robot_r**.

2. Launch everything using the commande :
```python
roslaunch assignment_2_2022 assign_python.launch
```
3. Download and run the notebook using : 
```python
jupyter-notebook --allow-root
```

4. From the interface you have the possibility to move the robot in different direction and see its path , also you can set a target and the robot to that target and you can cancel it any time you want, you can also see the bar chart for the reached and calceled targets.

### Implementation:

In order to accomplish the intended functionality, the notebook makes use of several libraries and techniques. The creation of interactive plots is facilitated by libraries such as matplotlib and FuncAnimation. Additionally, the rospy library is utilized to establish communication with the robot's navigation system. The nav_msgs.msg module is employed to subscribe to relevant topics like Odometry and LaserScan, which grant access to information pertaining to the robot's position and laser scanner data.

Here are the libraries and dependencies that were employed:
1.matplotlib: This library enables the creation of various types of plots and visualizations.
2.FuncAnimation: It provides functionality for animating plots in real-time.
3.rospy: This library allows for communication with the robot's navigation system using ROS (Robot Operating System).
4.nav_msgs.msg: This module provides message types for working with navigation-related topics, such as Odometry and LaserScan.
These libraries and dependencies play a crucial role in implementing the desired functionality within the notebook.


```python
from ipywidgets import VBox,HBox
import ipywidgets as widgets
import jupyros as jr
import rospy
from IPython.display import display, clear_output
import time
import numpy as np
from nav_msgs.msg import Odometry
from geometry_msgs.msg import  Twist
from robot_r.srv import my_service, my_serviceResponse
from sensor_msgs.msg import LaserScan 
from assignment_2_2022.msg import PlanningAction, PlanningGoal
from assignment_2_2022.msg import  PlanningActionResult, PlanningActionGoal,PlanningActionFeedback
from geometry_msgs.msg import PoseStamped
%matplotlib notebook
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation


```
### User Interaction

To enable user interaction with the robot's movement, the notebook incorporates buttons that correspond to different motion commands. These buttons provide users with the ability to initiate, halt, and adjust the robot's behavior within the environment. The notebook ensures that the robot's position and target tracking information are consistently updated to reflect any user-initiated modifications.

Specifically, four buttons are implemented to direct the robot in various directions. Additionally, an interface is provided to set a desired goal for the robot. Users can then choose to send the target or cancel it, thereby controlling the robot's navigation towards the specified goal. This user-friendly interface enhances the notebook's functionality by allowing users to actively participate in guiding the robot's movements and tracking its targets.

![Buttons](https://github.com/notMuizz/RT_2-JupyterNotebook/assets/123844091/e02bdd33-dccd-42f9-92e0-c4e0fd827228)
![goal_cancelled](https://github.com/notMuizz/RT_2-JupyterNotebook/assets/123844091/af42a416-754e-4969-aff5-edcea1ebd46f)


### Position and Target Tracking
In this section, a visual depiction of the robot's position and target positions is presented. By subscribing to pertinent topics and receiving position and status information, the plot is continuously updated. Real-time updates and animation of the plot are made possible through the utilization of FuncAnimation.

Code teste multiple times, and here is an example of the robot's path when it tries to avoid an obstacle to reach a target:

![possiblePathOvoidObstacle](https://github.com/notMuizz/RT_2-JupyterNotebook/assets/123844091/67a3f1ea-b8d4-4f2d-acaf-c4c79d9b59a7)


Text box to show the state of the goal. When the user sets a goal, it displays a message indicating the goal, and if the user cancels the goal, it shows a message canceling the goal.

![goal_cancelled](https://github.com/notMuizz/RT_2-JupyterNotebook/assets/123844091/95927fa8-6582-414a-843a-7aa6331b27ed)


### Target Tracking Status
Within the notebook, a bar chart is integrated to illustrate the count of reached and not-reached targets. This chart is dynamically updated in real-time by leveraging feedback from the robot's goal action client. Each bar in the chart represents a specific target status category, such as "Reached" and "Cancelled". The height of each bar corresponds to the count of targets within its respective category.

![CountReacheCanceled](https://github.com/notMuizz/RT_2-JupyterNotebook/assets/123844091/b87d8ff0-5b99-49ee-9849-a6cdb620a1af)



### Conclusion
To sum up, the Jupyter Notebook I developed offers a user-friendly and interactive platform for monitoring crucial aspects of the robot's operation, including its position, target tracking status, and closest obstacle distance. By incorporating widgets and visualizations, the notebook enhances the overall user experience by presenting information in a clear and concise manner. The replacement of the original user interface node with this notebook streamlines the process of controlling and tracking the robot's movement, making it more accessible and efficient for users.

