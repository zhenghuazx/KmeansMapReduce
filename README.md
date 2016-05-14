# KmeansMapReduce
#################################
Instructions for Hadoop Setup
#################################
If you already set up Hadoop, feel free to skip
this section as we do not require using the specific version or
configuration.
\url{http://hadoop.apache.org/docs/r1.2.1/single\_node\_setup.html}
has detailed instructions for setting up a hadoop on a single machine.

For Windows users, we recommend you try on a Linux system if possible
(you could install a Ubuntu on a virtual machine). Unfortunately if
Windows is your only choice, you may have to go through many hackings.

Here we emphasize some key steps that you need to take care of as you
walk through the instructions from the website.

1. The download section provides a list of Hadoop versions. We
recommend you download Hadoop version 1.2.1 from
\url{http://apache.mirrors.tds.net/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz}

2. After unzipping the folder, open \texttt{conf/hadoop-env.sh},
find line 9 \#export JAVA\_HOME=/usr/lib/xxxx, and
change it into export JAVA\_HOME=PATH\_TO\_YOUR\_JAVA\_HOME}. For Mac users, 
your Java path is probably ``/Library/Java/Home''. For Linux users, look for
your java path under ``/usr/lib/jvm/''.

3. Hadoop provides three modes. To test the code, you can use the
Pseudo-Distributed Mode. Pseudo-Distributed mode runs on a single
machine but simulates a distributed computing environment. If you 
have a cluster hdfs, then ignore this.

4.Before you proceed to setup the Pseudo-Distributed mode,
please follow the instructions in the ``StandAlone Operation''
section and make sure you can repeat the ``grep example''.

5. To configure the Pseudo-Distributed Mode, please follow the
"configuration" and ``Setup passpharaseless ssh''.

6. In the ``Execution'' step, notice there are extra steps:
$ bin/hadoop fs -put conf input,
$ bin/hadoop fs -cat output/ 
This is because in Pseudo-Distributed mode, the hadoop
program must read and write through HDFS (Hadoop Distributed File
System).  


You need to put the data files into HDFS. For
example, the code 'KmeansMRDriver.py' assumes the data is in the location:
hdfs:///user/yourusername/kmeans. You can import your data
into hdfs using the following commands:

bin/hadoop fs -mkdir kmeans bin/hadoop fs -put /PATH/TO/DATA/smallwiki/tfidf.txt kmeans/tfidf.txt 
bin/hadoop fs -put /PATH/TO/DATA/smallwiki/dictionary.txt kmeans/dictionary.txt
bin/hadoop fs -mkdir kmeans/cluster0 bin/hadoop fs -put /PATH/TO/DATA/smallwiki/cluster0.txt kmeans/cluster0/cluster0.txt

7. Follow the instructions in the ``Pseudo-Distributed
Mode'' section, and make sure you can repeat the ``grep example'' at
the end


#################################
Instructions for Starter Code
#################################
1. Download 'KmeansMapReduce'.
2. Update the path for hadoop and the path to the kmeans data within HDFS
   in the KmeansMRDriver.py file.
3. Run with  KmeansMRDriver.py

Remark: 
Between runs of kmeans, you will need to
remove the "kmeans/output" directory in hdfs:
 $ bin/hadoop fs -rmr kmeans/output
