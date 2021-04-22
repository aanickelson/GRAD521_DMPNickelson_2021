# Data Description:

The data set I will use is in a graph structure. Graphs consist of individual nodes that are connected by edges. An example graph is shown in the image below; circles are nodes and lines are edges. Each  node is grounded to a physical location in the map (maps in the simulation environment are usually on the scale of a building). Edges represent the connectivity between nodes.

<img src="https://github.com/aanickelson/GRAD521_DMPNickelson_2021/blob/main/graph_structure.png" width="400">

All of the data about the environment is stored within the graph structure and is all in simulation:
Node information
Location in space, described as an x,y coordinate pair and width / height
Edge information - some of the data (e.g. distance) is inherent to the physical grounding of the edges between two nodes. Other data is observed repeatedly within the environment
Two connecting nodes
Distances between two nodes - measured both by Euclidean and square distance
Observed data - 
Time to traverse an edge, with metadata about whether or not humans were present
Percent of time humans are present
Number of times the robot had a navigation failure (got lost) on that edge
Data are collected through a simulation environment called Gazebo utilizing the Robot Operating System (ROS). We will leverage the built-in navigation systems in ROS to allow the robot to navigate autonomously around the map environment. In order to simulate humans in the environment, a background script will randomly determine whether or not humans are ‘present’ on each edge; if they are present, the robot’s top speed will be throttled by a predetermined proportion. Another python script will be running to keep track of how long the robot takes to traverse each edge. These timings will be saved in the graph structure, as defined above. The graph structure will be saved as a [Pickle binary file](https://docs.python.org/3/library/pickle.html).

Data Size:
The graph containing the recorded data will be approximately 2 - 10 MB. We will likely record multiple data sets with different human presence conditions. In total, the data will not exceed 100MB.


# Roles and Responsibilities

# Data standards and metadata

# Storage and security

# Access and data sharing

# Archiving and preservation
