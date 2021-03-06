# Data Description:

**Data Types**

The data set I will use is in a graph structure. Graphs consist of individual nodes that are connected by edges. An example graph is shown in the image below; circles are nodes and lines are edges. Each  node is grounded to a physical location in the map (maps in the simulation environment are usually on the scale of a building). Edges represent the connectivity between nodes.

<img src="https://raw.githubusercontent.com/aanickelson/GRAD521_DMPNickelson_2021/main/graph_structure.png" width="400">

All of the data about the environment is stored within the graph structure and is all in simulation:
* Node information
  * Location in space, described as an x,y coordinate pair and width / height
* Edge information - some of the data (e.g. distance) is inherent to the physical grounding of the edges between two nodes. Other data is observed repeatedly within the environment
  * Two connecting nodes
  * Distances between two nodes - measured both by Euclidean and square distance
  * Observed data - 
    * Time to traverse an edge, with metadata about whether or not humans were present
    * Percent of time humans are present
    * Number of times the robot had a navigation failure (got lost) on that edge

**Data collection**

Data are collected through a simulation environment called [Gazebo](http://gazebosim.org/tutorials?tut=ros_overview) utilizing the [Robot Operating System (ROS)](https://www.ros.org/); both are open source platforms. We will leverage the built-in navigation systems in ROS to allow the robot to navigate autonomously around the map environment. In order to simulate humans in the environment, a background script will randomly determine whether or not humans are ‘present’ on each edge; if they are present, the robot’s top speed will be throttled by a predetermined proportion. Another python script will be running to keep track of how long the robot takes to traverse each edge. These timings will be saved in the graph structure, as defined above. The graph structure will be saved as a [Pickle binary file](https://docs.python.org/3/library/pickle.html).

**Data Size:**

The graph containing the recorded data will be approximately 2 - 10 MB. We will likely record multiple data sets with different human presence conditions. In total, the data will not exceed 100MB.


# Roles and Responsibilities

There are three responsible parties who take part in this research project: my advisor (PI), grad student (me), and one undergraduate student. For the data set listed in section one of this DMP, I am the main responsible party. The outline below details what my responsibilities are for each role described in class:


**Roles**

* **Archiving and preservation:** Archiving and preservation is done through Github in a team repository. The team repository is owned by the PI.
* **Protection of sensitive and protected data:** This is not applicable to this project. Our data are not sensitive and are readily available to the public.
* **Instrumentation maintenance:** this is not relevant to this project. All work is done in simulation on a lab computer. 
* **Data manager:** I am responsible for managing all data related to this research project. 
* **Data collection/data generation:** I am responsible for generating and collecting all data. 
* **Data organization, metadata generation, Quality control:** Again, I am entirely responsible for how the data are generated and organized, which includes metadata and quality control. My PI occasionally weighs in in high-level conversations, but the details are entirely up to me. 
* **Data analysis:** I take on the task of analyzing data. My PI occasionally weighs in on what different factors could suggest, but the hands-on data analysis is my responsibility. 
* **DMP implementation:** This has so far not been a factor in this research project. To my knowledge, there is no standing DMP that impacts my work. Going forward, my PI would be responsible for ensuring we meet any standards required by a DMP.
* **Access control:** My PI is responsible for the team github repository, which is how access control is managed.
* **Software creation and maintenance:** This is entirely on my shoulders. On rare occasions, I delegate some software creation responsibilities to the undergrad on my team. Maintenance is currently up to me. 

**Contingency plans:** 

There are currently no students in my lab who would take on this project after me. If / when I leave this project, the responsibilities will be handed over to my PI. My PI owns the group Github where this project is stored, so he already has access. I will provide documentation in the README to describe each file, the purpose, the metadata, and the procedures. If I know ahead of time that I am leaving (e.g. before graduation), I will initiate a formal hand-off to ensure he understands the data structure and procedures. 


# Data Standards and Metadata

**Standards**

There are no formal standards that apply to this project. However, there are widely agreed upon best practices or standards within the ROS community for file structure and naming. This will be discussed further in the Storage and Security portion below.

**Data Capture:**

* **Text file** - metadata about the simulation environment is stored in a plain text file along with the data, with appropriate headers and comments detailing each section.  
* **Python scripts** - For each data type, there is a matching python script that can process the data. The python script has extensive comments in the '__main__' section to explain the metadata (including units, plaintext explanation of the data type, etc). _Using the main section to provide detailed instructions on how to utilize the script and its associated files is considered best practice for Python._
* **README** - the README file includes information about how to launch the scripts, which python files perform which actions, and what data is collected. 

The following are a few examples of metadata recorded for this project:
* **Naming scheme** - the naming scheme is outlined in the python script that processes the text file associated with the simulation environment. In this specific naming scheme, each node is listed as either a room ('r'), hallway ('h'), or exclusion zone ('ex'); rooms all have associated doorways ('d'). Exclusion zones are portions of the simulation environment that are inaccessable. Each node in a subcategory is then assigned a two digit number starting at 00. For example, the second door in the fourth room would be named 'r03_d01'; the first hallway is 'h00'.
* **Recorded data** - The main script for processing data shows an example of how to read and use each type of data. It also includes comments detailing the data types and formats. For example, there are two arrays "trav_data_hum" and "trav_data_no" that record the traversal times when humans are present (hum) or absent (no), respectively. The metadata in the python file details which is associated with human presence, as well as information about the data type (numpy array). Each of these arrays also has an associated mean 'mean_hum' and 'mean_no' and standard deviation 'std_hum' and 'std_no'. All variables have a similar naming scheme to make it easily understandable. Naming schemes are included in the comments of the python file. 

# Storage and Security

**Access**

Our data for this project are not confidential and do not require protection. They are open source and available to the public on github through our lab's github group page ([Oregon State University Personal Robotics Group](https://github.com/osuprg)). The repository for this project can be found here: https://github.com/osuprg/hospital-world

**Storage and retention**

This project is publicly available on Github and will remain there in perpetuity. The main repository is on github. This repository is owned by the PI on the project, so the files will still be available to the lab when I leave. There is a copy of the repository local on my research machine, which is owned by the lab. Any changes to the local repository are manually pushed to github utilizing the UI interface in Pycharm. This is done every 1-3 hours and at the end of the day on days that I am working on code or the data. 

**Organization**

Though there are no formalized standards that apply to this project, ROS users have a widely agreed upon informal file structure. The file structure will follow this informal standard file structure for ROS workspaces. Version control is handled both through Git versioning and by appending a date to relevant data file names. All files with recorded data will be appended with the date in YYYY-MM-DD format. 

Directories will include:
* **Launch** - [ROS launch files](http://wiki.ros.org/roslaunch) (these spin up multiple scripts alongside the simulated environment) 
* **Scripts** - custom ROS files / scripts 
* **Worlds** - custom simulation environments
This project will include the following additional sub-directories:
* **Pickles** - Data recorded from simulation tests, stored in the pickle (.pkl) format

**Version Control**

Version control is primarily handled through git's built in versioning system. We additionally include the date and time stamp in the file name for all generated data in order to differentiate the data sets.

# Access and Data Sharing

**Access**

As discussed in the previous section, there are no limits on sharing this data. The data are currently publicly available on Github. A link to the Github will be included in all documentation and papers going forward. There are no privacy or confidentiality issues, as all data are generated in simulation by the robot. All data are in python files, plain text, or python pickle files, all of which are open source formats. We will utilize the MIT license and allow reuse as long as there is direct attribution. The README file for the repository will include this information.

**Archiving and Preservation**

Data will be archived and preserved in our group Github account, which is also how it is made available. That Github account will remain active for the foreseeable future. Archiving and preservation are identical to storage, as it utilizes the same formats and system. 

