# **MapReduce**

#### **Q1. Explain the concept of MapReduce program for a word count task with suitable Python / Java program.**

**Concept:**
MapReduce is a programming model used for processing large datasets in parallel across distributed clusters.

**Word Count Logic:**

* **Map Step**: Reads lines of text and emits each word with a count of 1
  → Output: `(word, 1)`
* **Shuffle & Sort**: Groups all values for the same word
* **Reduce Step**: Adds up the counts for each word
  → Final Output: `(word, total_count)`

---

### **Python (using Hadoop Streaming):**

```python
# mapper.py
import sys
for line in sys.stdin:
    for word in line.strip().split():
        print(f"{word}\t1")
```

```python
# reducer.py
import sys
from collections import defaultdict
counts = defaultdict(int)
for line in sys.stdin:
    word, count = line.strip().split("\t")
    counts[word] += int(count)
for word in counts:
    print(f"{word}\t{counts[word]}")
```

**Command to Run (Hadoop Streaming):**

```bash
hadoop jar hadoop-streaming.jar \
  -mapper mapper.py \
  -reducer reducer.py \
  -input input_dir \
  -output output_dir
```

---

### **Java (Classic Hadoop MapReduce):**

```java
public class WordCount {
  public static class Map extends Mapper<LongWritable, Text, Text, IntWritable> {
    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();
    public void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
      for (String str : value.toString().split("\\s+")) {
        word.set(str);
        context.write(word, one);
      }
    }
  }

  public static class Reduce extends Reducer<Text, IntWritable, Text, IntWritable> {
    public void reduce(Text key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
      int sum = 0;
      for (IntWritable val : values) {
        sum += val.get();
      }
      context.write(key, new IntWritable(sum));
    }
  }
}
```

---

**Summary Tip for Exam:**

* **Map** → Split and emit word with count 1
* **Reduce** → Aggregate word counts
* **Used in** → Word count, log analysis, sorting, indexing

