export HADOOP_CLASSPATH=${JAVA_HOME}/lib/tools.jar


-- COMPILE
hadoop com.sun.tools.javac.Main ClassAverage.java

jar cf ca.jar ClassAverage*.class



-- MAKE DIR
hadoop fs -mkdir /user/tipparac/classaverage
hadoop fs -mkdir /user/tipparac/classaverage/input
hadoop fs -mkdir /user/tipparac/classaverage/output

hadoop fs -copyFromLocal /home/tipparac/DataSet /user/tipparac/classaverage/input/DataSet

hadoop fs -copyToLocal /user/tipparac/classaverage/output/part-r-00000 /home/tipparac/part-r-00000

hadoop fs -copyToLocal /user/tipparac/classaverage/output /home/tipparac/output


-- EXECUTE
hadoop jar ca.jar ClassAverage /user/tipparac/classaverage/input /user/tipparac/classaverage/output /user/tipparac/classaverage/logs 2



hadoop fs -ls /user/tipparac/classaverage/output/
hadoop fs -ls /user/tipparac/classaverage/logs/

hadoop fs -rm -r /user/tipparac/classaverage/output/

-- READ STUFF
hadoop fs -cat /user/tipparac/classaverage/output/part-r-00000

hadoop fs -cat /user/tipparac/classaverage/logs/results.txt