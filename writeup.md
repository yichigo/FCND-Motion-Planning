## Project: 3D Motion Planning

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.  

You're reading it! Below I describe how I addressed each rubric point and where in my code each point is handled.

### Explain the Starter Code
"motion_planning.py" is the main program.
"planning_utils.py" include some functions we need to plan the path.
"planning_utils.py" has been included in "motion_planning.py"
Both of them are combined with some programs we used in the previous sections such as "backyard_flyer_solution.py" and "A-Star.ipynb"


#### 1. Explain the functionality of what's provided in `motion_planning.py` and `planning_utils.py`
These scripts contain a basic planning implementation that includes...

### In "planning_utils.py":
create_grid(): create a grid for the map
Action(): the move of nest step
valid_actions(): for the next move, check if the node is off the grid or it's an obstacle 
a_star(): search the path by using A-Star algorithm
heuristic(): the estimated distance between a point and the goal point.

And two functions are added:
1.read_home(filename): read the first line from a file, and return latitude, longtitude.
2.prune_path(path): delete the redundant points in a straight line

### In "motion_planning.py"
plan_path(): the main progress of path plan, combined with data reading, map to grid creating, a_star(),  prune_path(), etc.
The code I added are:
line 123-124: read lat0, lon0 from "colliders.csv"
line 126: set home position to (lon0, lat0, 0)
line 131: convert global location to local location
line 137-138: create a grid for the map
line 142-143: set the start point in grid
line 149-150: set the goal point in grid
line 145-155: find a path by using A-Star algorithm, which has been included in "planning_utils.py".
line 159: delete the redundant points in the path
line 167: send waypoint to sim
line 187-189: set the goal point at the beginning of the main program.

### Implementing Your Path Planning Algorithm

#### 1. Set your global home position
line 123-124: read lat0, lon0 from "colliders.csv" by using function read_home(), which has been defined in "planning_utils.py".
line 126: set home position to (lon0, lat0, 0) by using function self.set_home_position()

#### 2. Set your current local position
line 131: convert global location to local location by using function global_to_local()

#### 3. Set grid start position from local position
line 137-138: create a grid for the map
line 142-143: set the start point in grid

#### 4. Set grid goal position from geodetic coords
line 149-150: set the goal point in grid

#### 5. Modify A* to include diagonal motion (or replace A* altogether)
In "planning_utils.py":
line 60-63: create 4 direction with cost = sqrt(2)
line 94-101: For these new 4 directions, check if the node is off the grid or it's an obstacle

#### 6. Cull waypoints 
line 159: detete the redundant points by using function prune_path(), which has been created in "planning_utils.py".  I delete the redundant points in a straight line.

### Execute the flight
#### 1. Does it work?
It works!

### Double check that you've met specifications for each of the [rubric](https://review.udacity.com/#!/rubrics/1534/view) points.
  
# Extra Challenges: Real World Planning

For an extra challenge, consider implementing some of the techniques described in the "Real World Planning" lesson. You could try implementing a vehicle model to take dynamic constraints into account, or implement a replanning method to invoke if you get off course or encounter unexpected obstacles.
