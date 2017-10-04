# Path Planning in Highway
This is a simple path planning project that plans a car driving in a highway.

The macro path-planning data(map way points) has been provided by Udacity so I don't need to implement this part. What I only need to implement is the micro path-planning that gives a specific trajectory to a car to follow in order to performance a certain behaviour(go straight, change lane, or slow down) while obeying the basic rules(no collision, no exceed the max acceleration and jerk, keep lane) and maintaining the efficiency(keep the velocity around the 50 mph).

## Rules Obeying
For smoothing the path and make sure not exceed the max jerk, I used the open source spline library(as cited in my code) written by ttk592. The points used in generating spline are: last 2 points in previous path to be consistent with history and avoid shaking, and new anchor points for next 30, 60, 90 meters.

Setting d value to (lane * 4 + 2) to make sure that car is driving in the middle of the lane.

## Behaviour Planning
Sometimes there's another car in front of my car. To maintain the efficiency, it's better to change the lane.

To plan the lane changing, first, I need to calculate the distances of the nearest car in each lane and pass it to my behaviour planning function.

To calculate the distances of the nearest car in each lane, I used qitong's solution as cited in my code.

Then it's my implementation of behaviour planning. First, check the distance of the nearest car in current lane. If it does not go beyond the slow down threshold(where I set 18.0), let the car keep in current lane. If not, it would check the left lane and right lane with the same checking pipeline. If change lane left or right is okay, then change it. Else(there're cars very near in my front, left, and right, like in a traffic jams), the car would keep in current lane and slow down.

## Result
The car successfully drive around the whole track without breaking any rules. It would automatically change the lane if there're cars in front of it and slow down if there're too many cars in the front, left, and right of it.

## Future performances
Change the slow down threshold that can improve the car's efficiency in crowd traffics. Also, in this project, I assume that all cars go straight. Actually, other cars may change lanes too. Add prediction parts may improve the car's efficiency.

I think instead of rule-based approaches, deep reinforcement learning is a better approach.

