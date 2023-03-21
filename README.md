# Prerequisite
1)Make sure your terminal at the main app folder directory

# Data Source
**Pull data from API**

PS : Use docker images to check Images ID

1) docker run -v C:\Users\USER\Desktop\FypApp\DataStorage\data:/app/data (Python Script Image ID)
2) file should be in FypApp\DataStorage\data

# Data Storage
**Store Data in NameNode**

PS : Use docker ps to check container ID

1) docker cp C:\Users\USER\Desktop\FypApp\DataStorage\data\data_australia.csv (namenode Container ID):/tmp

**Make hdfs directory**

2) docker exec -it namenode /bin/bash

3) hdfs dfs -mkdir -p /data

**Store Data in hdfs**

4) hdfs dfs -put /tmp/data_australia.csv /data/data_australia.csv

**Check if Data is stored in hdfs**

5) hdfs dfs -ls /data

PS: to leave from root of namenode use Ctrl-Z

# Batch Processing

PS : Use docker ps to check container ID

**To go into spark**

1) docker exec -it (spark Container ID) bash

2) inside bash use spark-shell

**Load Data from HDFS**

3) val df = spark.read.csv("hdfs://namenode:9000/data/data_australia.csv")

PS: to leave from Scala cmd use Ctrl-D
PS: to leave from bash cmd use Ctrl-Z

# Data Visualization

1) docker cp C:\Users\USER\Desktop\FypApp\DataStorage\data\weather.csv (namenode Container ID):/weather.csv

2) docker run -p 8501:8501 fypapp-visualizeapp