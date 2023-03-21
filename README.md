# GeoSpatial_Hackathon-StartUp_Challenge_By_IIIT-Hyderabad
Contactless Enforcement Solutions For Cycle Lanes to promote Active Mobility in India as safe as possible.


**1. A detailed description of the scope of the solution**

**-----------------------------------------------------------**

In the case of CCTV, as its location is fixed and its hardware performance is superb, it is highly effective for the monitoring of car movements in a predefined area. 

A number of video surveillance devices used for traffic condition analysis, people identification , and event detection. As they are dealing with a single video source, the analysis results were limited, and combining the results from separate video sources would be both time-consuming and labor-intensive. Vehicle tracking based on surveillance videos suffers from the same problem. 

To solve this, I propose a Kafka-based real-time vehicle tracking system that can collect data from different video sources, extract relevant features from vehicles for monitoring, and integrate them in a consistent manner.

The effectiveness of vehicle tracking relies on diverse information, such as 
plate number
time
place
direction
collected from numerous different places. 

Fortunately, modern CCTV cameras provide diverse metadata including global positioning system (GPS) and time-stamping. 

In addition, plate number and moving direction can be easily detected from the captured images using popular image processing or machine learning techniques.

————-xx————-xx————

Real-time vehicle tracking system based on surveillance videos from diverse devices including CCTV, dashboard cameras, and drones. 

For scalability and fault tolerance, our system is to be built on a distributed processing framework and comprises a Frame Distributor, a Feature Extractor, and an Information Manager. 

The Frame Distributor is responsible for distributing the video frames from various devices to the processing nodes. 

The Feature Extractor extracts principal vehicle features such as plate number, location, and time from each frame. 

The Information Manager stores all the features into a database and handles user requests by collecting relevant information from the feature database. 

To illustrate the effectiveness of our proposed system, we implemented a prototype system and performed a number of experiments. I report some of the results mentioned below. 

————-xx————-xx————

An integrated vehicle tracking system, IVATS, based on Kafka and HBase was designed and developed. 

Our system could assign a significant number of frames from diverse video sources, such as CCTVs cameras, to processing nodes using Apache Kafka. 

Primary vehicle features such as plate number, time, and location data were extracted accurately from the frames using image and metadata processing. 

The feature data were stored in HBase clusters and retrieved for query processing. 

For effective query processing, an indexing structure based on R-Tree was proposed. 

In the experiments, I demonstrate that our system can handle diverse user queries, including vehicle tracking and traffic congestion, efficiently. 

Based on the data distribution, storage structure, Rowkey design, and indexing structure, our system can effectively handle real-time requirements of vehicle tracking applications. 

————-xx————-xx————

**2. Improvements in functional PoC over Phase 1 submission**

Drawbacks:
It is not easy to implement for a number of reasons. 

Firstly, the system should have sufficient storage and processing capacity to handle the big data involved. 
The volume of data generated from the video devices in real time is significant. 
Therefore, the system should be sufficiently fast to avoid any data accumulation inside the node, otherwise, all the nodes in the system could experience a memory shortage and, in the worst case, the entire system might stop. 
To overcome this problem, a distributed processing platform can be used. 

Secondly, the system should have a fault tolerance ability that is essential for the system to provide accurate and complete car tracking information. 
This means that when a node fault or transmission fault occurs, the system should be able to recover from the fault. 

Thirdly, precise and fast image processing methods should be supported to efficiently extract all the critical information about the cars in the frames. 

Finally, to answer user queries promptly, the system should have methods for managing a significant amount of data efficiently, including an index structure for query processing.

We investigated methods for recognising or tracking automobiles from video frames.
As numerous diverse vehicle feature extraction methods have been developed, complete systems for vehicle tracking have also been proposed. 
A system that collected the frames from surveillance videos, recognised the license plate, and provided the results to the user that consequently enabled remote monitoring.
One proposed a video surveillance system in a cloud environment. Because of the automatic license plate recognition engine and the cloud environment, their system was able to cover wide areas and visualised the detection results using Google Maps.

We investigated frameworks for real-time distributed processing. 
Hadoop processes data in batches, HIPI (Hadoop image processing interface) is not appropriate for real-time processing. In addition, the Hadoop distributed file system uses a random-access approach to disks, which induces an amount of delay in accessing the data in a file system. 
Spark is one of the fastest frameworks for suitable for distributed processing. However, it has a critical weakness with insufficient memory. When it encounters insufficient memory, the processing speed of the system decreases rapidly and could even result in the data in the memory being lost. 
The abovementioned disadvantages of the two popular frameworks could be significant stumbling blocks for real-time vehicle tracking. 

Therefore, I focused on Kafka, which is a platform developed for real-time message transmission. Kafka comprises three parts: Producer, Consumer, and Broker. 
Producer generates data and sends them to the Broker. 
In Broker, the data are classified according to their topics and replicated for in- creased reliability. 
Consumer, a processing part, obtains the data from Broker each time it finishes tasks.
 
Kafka has the following properties: 
It stores temporary data in its own file system
Each Consumer schedules its own task 
Saving data in the storage nodes enables Kafka to recover the data without data loss when an error occurs. 
Although memory-based structures are typically faster than disk-based structures, the speed of data access in Kafka is comparable to that of memory-based structures because of efficient disk usage. 

The second property indicates that a Kafka node need not wait for a job schedule from the cluster master. Therefore, bottleneck problems caused by scheduling can be avoided and the communication between nodes can be decreased, reducing the network load. 

Because of these properties, Kafka can be a suitable framework in a real-time environment, and it was validated. 

We investigated distributed databases, and index structures for HBase.
Due to popularity of distributed processing frameworks, distributed databases like Cassandra, MongoDB, and HBase are attracting increasing attention for managing large volumes of data. 
MongoDB is another open-source cross-platform NoSQL database program & is a categorized as document-based database.
While Cassandra and HBase are column-based databases. Compared to other database management systems, it is easy to use and can process a number of query conditions. 

HBase is an open-source, non-relational database based on Hadoop and Google Bigtable. 

It ensures data consistency and provides fault tolerance. 
HBase is based on Hadoop, it is easy to use MapReduce when implementing the various query processing methods. 
For this reason, we use HBase for data management. 

In HBase, a data tuple is called a row and data are managed in tables that are divided into small row sets known as region. 
Therefore, MapReduce performs data processing in the unit of region. 
Except for Rowkey, which is an identifier of a row, the attributes of a table are not indexed. This means that HBase must access all stored data to answer user queries. 
Therefore, data retrieval takes significantly longer than data insertion and the query processing time increases rapidly as the volume of stored data increases. 
To overcome this problem, a number of studies have proposed the index structure, specifically for geometric information. 
A popular index structure for geometric information is R-tree-based indexing scheme for trajectory data of cars in a distributed environment. However, we optimised the index structure by indexing GPS data using Quad-tree-based indexing scheme and Hilbert space-filling curves to obtain improved performance. 


**3. What are the technologies used in the functional PoC?**

I propose a real-time vehicle tracking system IVATS (Integrated Video-based Automobile Tracking System) that can collect video big data, extract and store principal vehicle features, and process user queries in a real-time environment. 

Our proposed system comprises three components: Frame Distributor (FD), Feature Extractor (FE), and Information Manager (IM). 
FD is responsible for reliable distribution of the video frames from a number of devices to the processing nodes. (The role of the FD is to assign a significant amount of frames from numerous video sources to processing nodes using Apache Kafka) 
FE extracts diverse vehicle features such as plate number, time, and location from each frame. (Each node in the FE extracts principal vehicle features such as plate number, time, and location from the frame and transfers them to the IM)
IM stores all the extracted feature data, processes user queries by collecting relevant information from the feature database, and presents the query results to the user. (The IM that is built on HBase clusters is responsible for storing all the extracted features, constructing index structures for them, and retrieving all the relevant data to answer user queries)

Overall structure of IVATS:

![image](https://user-images.githubusercontent.com/108155749/226162739-341c0ba8-8502-49e5-8734-15d3f7e8802f.png)
