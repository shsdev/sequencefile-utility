sequencefile-utility
====================

Introduction
------------

This is a utility for creating a Hadoop SequenceFile. Files are either 
collected by recursively traversing a root directory or using a Hadoop job.

Installation requirements
-------------------------

In order to build the application, Java SE Development Kit (JDK) version 
>=1.6.0 and Apache Maven >= 2.2.1 is required. 

Installation
------------

Compile project using maven:

    mvn install

Usage
-----

    {hadoop jar|java -jar} target/sequencefile-utility-1.0-jar-with-dependencies.jar [-c <arg>] [-d <arg>] [-e <arg>] [-h] [-m] [-n <arg>] [-p <arg>] [-t]
 
-c,--compr <arg>   Compression, one of NONE,RECORD,BLOCK, default: BLOCK
                    (Optional).
 -d,--dir <arg>     Local directory (or directories - commaseparated)
                    containing files to be added. Note that in hadoop map
                    mode (parameter -m) each tasktracker must be able to
                    access the files at the same path. (Required)
 -e,--ext <arg>     Extension filter(s) - commaseparated (Optional).
 -h,--help          print this message.
 -m,--mapmode       Hadoop map mode: A text file containing all absolute
                    paths of the input directory (parameter -d) is created
                    and the sequence file is created using a map/reduce
                    job. The sequence file is direcly stored in HDFS. If
                    this parameter is omitted, the sequence file creation
                    runs as a batch process, adding all files of a
                    directory to a sequence file (one per directory) in a
                    separate thread. (Optional)
 -n,--name <arg>    Hadoop map mode: Hadoop job name (Optional)
 -p,--path <arg>    Hadoop map mode: HDFS input path where the text files
                    containing input paths is available. If this parameter
                    is provided, the -d parameter is not required
                    (Optional)
 -t,--textline      Text line mode, input files aretext files and each
                    line of the text files should be added as a record in
                    the sequence file (Optional).