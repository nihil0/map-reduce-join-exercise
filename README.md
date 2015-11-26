# Hadoop Platform and Application Framework

## Week 4: Introduction to Map/Reduce

### Assignment: Joining Data

Since the formatting and exercise description is very poor, here is a detailed tutorial version of the exercise from [this](https://www.coursera.org/learn/hadoop/home/welcome) Coursera course with all files included. Just clone this into your home folder on the Cloudera Quickstart VM and you're all set!

#### Exercise in Joining data with streaming using Python code:


In Lesson 2 of the Introduction to Map/Reduce module the Join task was described. In this assignment, first you are given a Python mapper and reducer to perform the Join described in the video (3rd video of lesson). The purpose of the first part of this assignment is mostly to provide an example for the second part. Your second assignment will be to modify that Python code (or if you are so inclined write one from scratch) to perform a different Join. You will asked to upload an output file(s).

Please read through all the instruction and if you are not a programmer, especially the programming notes. It is not a hard programming assignment, but I believe worth the effort to understand the nature of map/reduce framework.


Part 1
=======

**Step 1** : Make the Python scripts for the mapper and reducer executable. Execute the following commands (printed in one line here for ease of copying and pasting):

```
chmod +x join1_mapper.py && chmod +x join1_reducer.py
```

**Step 2**: Test the program in serial execution my executing the fllowing command: 

```
cat join1_File*.txt | ./join1_mapper.py | sort | ./join1_reducer.py
```

 Explanation: `cat join1_File*.txt` prints out the contents of the files `join1_FileA.txt` and `join1_FileB.txt` to the [Standard Output Stream](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_.28stdout.29). The "pipe" operator `|` redirects the data to be written to the output stream to the script `join1_mapper.py`. The next pipe directs the output of `join1_mapper.py` to the built-in program `sort`, which sorts the lines of the output of `join1_mapper.py` in alphabetical order. The output of the `sort` program is then piped to `join1_reducer.py` which prints its output to the system's standard output. 

**Step 3** : Run the following commands to put the data files `join1_FileA.txt` and `join1_FileB.txt` into the Hadoop Distributed File System. You can also do this graphically using HUE. 

Create a folder called "input"

```
hdfs dfs -mkdir /user/cloudera/input
```

Put the first file in
```
hdfs dfs -put ~/map-reduce-join-exercise/join1_FileA.txt /user/cloudera/input/
```

Now the second one
```
hdfs dfs -put ~/map-reduce-join-exercise/join1_FileB.txt /user/cloudera/input/
```

** Step 4** : Run the map-reduce job using the following command (on one line to prevent line-break issues):

```
hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar -input /user/cloudera/input -output /user/cloudera/output_join  -mapper /home/cloudera/join1_mapper.py -reducer /home/cloudera/join1_reducer.py
```
