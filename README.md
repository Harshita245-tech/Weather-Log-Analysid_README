
# README - Weather Log Analysis using Hadoop

## 📌 Project Overview  
This project implements Weather Log Analysis using Hadoop MapReduce. The goal is to analyze weather logs and find the maximum temperature recorded per year.

## 📂 Directory Structure  
```
📁 Weather_Log_Project/
│── 📜 weather_mapper.py   # Mapper script
│── 📜 weather_reducer.py  # Reducer script
│── 📄 weather_logs.txt    # Sample input weather data
│── 📄 README.md           # Documentation file
```

## 🛠 Prerequisites  
Ensure you have the following installed:  
- Hadoop (version 3.4.0 or later)  
- Python (version 3.x)  

---

## 🔹 Start Hadoop Services  
```bash
bin/start-all.sh
jps
```
Expected Output:
```
20309 NameNode  
20725 SecondaryNameNode  
20518 DataNode  
20845 JobTracker  
21181 Jps  
21071 TaskTracker  
```

---

## 🔹 Create Mapper and Reducer Scripts  
```bash
nano weather_mapper.py
nano weather_reducer.py
chmod +x weather_mapper.py
chmod +x weather_reducer.py
```

---

## 🔹 Upload Input Files to HDFS  
```bash
hdfs dfs -mkdir -p /weather_logs
hdfs dfs -put weather_logs.txt /weather_logs
```

---

## 🔹 Run Hadoop MapReduce Job  
```bash
hadoop jar $HADOOP_HOME/share/hadoop/tools/lib/hadoop-streaming-3.4.0.jar \
    -input /weather_logs/ -output /weather_output \
    -mapper ~/weather_mapper.py -reducer ~/weather_reducer.py
```

### Possible Error  
If the output directory already exists, rename or delete it:  
```bash
hdfs dfs -rm -r /weather_output
```
Then, rerun the job.

---

## 🔹 Check Output in HDFS  
```bash
hdfs dfs -cat /weather_output/part-00000
```

### ✅ Expected Output:  
The final output contains the maximum temperature recorded per year.

```
2020 35.1
2021 30.5
2022 33.0
```

---

## 🔹 Upload Output Image for Visualization  
```bash
hdfs dfs -put output_chart.png /weather_result/
```

---

## 🔹 Stop Hadoop Services  
```bash
bin/stop-all.sh
```
Expected Output:  
```
Stopping namenode  
Stopping datanode  
Stopping secondarynamenode  
Stopping jobtracker  
Stopping tasktracker  
```

---

## 🎯 Conclusion  
This project demonstrates how to execute a Hadoop-based MapReduce program for Weather Log Analysis.  

