Absolutely! Here’s a step-by-step guide to **run your Hadoop WordCount program**:

---

## 1. **Prerequisites**

- **Hadoop** installed and configured (standalone, pseudo-distributed, or cluster mode).
- **Java** installed (JDK 8 or later recommended).
- Your Java code saved as `WordCount.java`.

---

## 2. **Compile the Code**

First, you need to compile your Java code and package it into a JAR file.

```bash
# Set HADOOP_HOME and add Hadoop libraries to the classpath
export HADOOP_HOME=/path/to/hadoop
export PATH=$PATH:$HADOOP_HOME/bin

# Compile the code
javac -classpath `${HADOOP_HOME}/share/hadoop/common/hadoop-common-*.jar`:`${HADOOP_HOME}/share/hadoop/mapreduce/hadoop-mapreduce-client-core-*.jar` -d wordcount_classes WordCount.java

# Create a JAR file
jar -cvf wordcount.jar -C wordcount_classes/ .
```

---

## 3. **Prepare Input Data**

Create a sample input text file:

```bash
echo "hello world hello hadoop" > input.txt
```

Create an input directory in HDFS and put your file there:

```bash
hadoop fs -mkdir -p /user/yourusername/input
hadoop fs -put input.txt /user/yourusername/input/
```

---

## 4. **Run the MapReduce Job**

Run your WordCount job using the Hadoop command:

```bash
hadoop jar wordcount.jar WordCount /user/yourusername/input /user/yourusername/output
```

- Replace `/user/yourusername/input` with your actual input path in HDFS.
- `/user/yourusername/output` is the output directory (should **not exist** before running).

---

## 5. **View the Output**

After the job completes, check the output:

```bash
hadoop fs -ls /user/yourusername/output
hadoop fs -cat /user/yourusername/output/part-r-00000
```

You should see the word counts, e.g.:

```
hadoop 1
hello 2
world 1
```

---

## 6. **Troubleshooting**

- If you get a "class not found" error, ensure your JAR contains the compiled classes and the package structure matches.
- If the output directory exists, Hadoop will throw an error. Delete it first:
  ```bash
  hadoop fs -rm -r /user/yourusername/output
  ```

---

## **Summary Table**

| Step              | Command/Action                                                                 |
|-------------------|--------------------------------------------------------------------------------|
| Compile           | `javac -classpath ... -d wordcount_classes WordCount.java`                      |
| Package           | `jar -cvf wordcount.jar -C wordcount_classes/ .`                                |
| Prepare Input     | `hadoop fs -mkdir -p ...` and `hadoop fs -put ...`                              |
| Run Job           | `hadoop jar wordcount.jar WordCount /input/path /output/path`                   |
| View Output       | `hadoop fs -cat /output/path/part-r-00000`                                      |

---

**Let me know if you want commands for Windows, or if you have a specific Hadoop version or cluster setup!**

---
Answer from Perplexity: https://www.perplexity.ai/search/import-java-io-ioexception-imp-xh1uAkeYSxGHTfUR_6P05Q?utm_source=copy_output
