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

hadoop_namenode:/hadoop/dfs/name


**Run new instance of Streamlit container**
docker run -p 8501:8501 fypapp-visualizeapp
**Copy from HDFS to local storage**
docker cp (namenode container id):tmp\weather.csv C:\Users\taskin.intern\"OneDrive - Razer (Asia-Pacific) Pte. Ltd"\Desktop\weather.csv
**Copy from local storage to streamlit container**
docker cp C:\Users\taskin.intern\"OneDrive - Razer (Asia-Pacific) Pte. Ltd"\Desktop\weather.csv (visualizer Container ID):/weather.csv

**Some useful commands**
docker ps --format "{{.Names}}"
C:\Users\taskin.intern\"OneDrive - Razer (Asia-Pacific) Pte. Ltd"\Desktop\tmp
C:\"Program Files (x86)"\FypApp\FypApp\DataStorage\data


**Option to use volumes**
*Copy from hdfs to streamlit via shared volume*
docker volume create shared_volume
docker run -it --name hdfs_container -v shared_volume:/shared hdfs_image
docker exec -it hdfs_container bash
hdfs dfs -copyFromLocal /path/to/local/file /shared/file
docker run -it --name streamlit_container -v shared_volume:/shared streamlit_image
docker exec -it streamlit_container bash
cat /shared/file
