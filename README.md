sequencefile-utility
====================

Introduction
------------

This is a utility for creating a Hadoop SequenceFile. The utility can be 
used either as a local command line application that collects files recursively 
by traversing a root directory. Or it can be used as a Hadoop job where 
data is collected in the Map task (requires that the file system is mounted 
on all TaskTracker nodes).

Installation requirements
-------------------------

In order to build the application, the Java SE Development Kit (JDK) version 
1.6.0 (or higher) and Apache Maven 2.2.1 (or higher) are required. 

Installation
------------

Compile project using maven:

    mvn install

Usage
-----

    {hadoop jar|java -jar} target/sequencefile-utility-1.0-jar-with-dependencies.jar 
    [-c <arg>] [-d <arg>] [-e <arg>] [-h] [-m] [-n <arg>] [-p <arg>] [-t]
 
* `-c,--compr <arg>`
    * Compression, one of NONE,RECORD,BLOCK, default: BLOCK (Optional).
* `-d,--dir <arg>`     
    * Local directory (or directories - commaseparated)
      containing files to be added. Note that in hadoop map
      mode (parameter -m) each tasktracker must be able to
      access the files at the same path. (Required)
* `-e,--ext <arg>`     
    * Extension filter(s) - commaseparated (Optional).
* `-h,--help`          
    * Print this message.
* `-m,--mapmode`       
    * Hadoop map mode: A text file containing all absolute
      paths of the input directory (parameter -d) is created
      and the sequence file is created using a map/reduce
      job. The sequence file is direcly stored in HDFS. If
      this parameter is omitted, the sequence file creation
      runs as a batch process, adding all files of a
      directory to a sequence file (one per directory) in a
      separate thread. (Optional)
* `-n,--name <arg>`    
    * Hadoop map mode: Hadoop job name (Optional)
* `-p,--path <arg>`    
    * Hadoop map mode: HDFS input path where the text files
      containing input paths is available. If this parameter
      is provided, the -d parameter is not required
      (Optional)
* `-t,--textline`      
    * Text line mode, input files aretext files and each
      line of the text files should be added as a record in
      the sequence file (Optional).

Examples
--------

Read all files from a local directory into one sequence file:

    java -jar target/sequencefile-utility-1.0-jar-with-dependencies.jar -d /path/to/dir/ -c NONE

Use a Hadoop job to read all files from a file system that is mounted on all
Task Tracker nodes:

    hadoop jar target/sequencefile-utility-1.0-jar-with-dependencies.jar -m -n hadoopjob -p /path/to/hdfs/dir -c NONE

The `-p` parameter indicates a HDFS input path where text file(s) are located 
that contain absolute paths to the files that should be packaged in the SequenceFile.