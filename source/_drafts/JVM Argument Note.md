JAVA_CNF="
-server 
-Xmx3072M 
-Xms3072M 
-Xmn1536M 
-Xss320k 
-XX:+UseThreadPriorities		// This option enables you to control the priority of Java threads using java.lang.Thread.setPriority() and related APIs. If this feature is disabled, using these APIs has no effect.

-XX:ThreadPriorityPolicy=1 
-XX:+UseParNewGC 				// Enables the use of parallel threads for collection in the young generation. Replace UseConcMarkSweepGC after JDK 1.8
-XX:+UseConcMarkSweepGC 		// Use concurrent mark-sweep collection for the old generation. (Introduced in 1.4.1)
-XX:+CMSParallelRemarkEnabled   // The option CMSParallelRemarkEnabled means the remarking is done in parallel to program execution
-XX:SurvivorRatio=8 \			// Ratio of eden/survivor space size. The default value is 8.
-XX:MaxTenuringThreshold=1 		// Maximum value for tenuring threshold. The default value is 15.
-XX:CMSInitiatingOccupancyFraction=75 
-XX:+UseCMSInitiatingOccupancyOnly 
-Dfile.encoding=UTF-8 \
-XX:ErrorFile=./log/java_error%p.log 
-XX:+HeapDumpOnOutOfMemoryError \
-Xloggc:$GC_FILE_NAME 
-verbose:gc 
-XX:+PrintGCDetails 
-XX:+PrintGCDateStamps 
-XX:+PrintGCTimeStamps 
-XX:+UseGCLogFileRotation 
-XX:NumberOfGCLogFiles=10 \



JAVA_CNF="
-server 
-Xmx512M 
-Xms512M 
-Xmn256m 
-Xss256k 
-XX:PermSize=128m 
-XX:LargePageSizeInBytes=4m
-XX:ParallelGCThreads=8 
-XX:+UseG1GC 
-XX:MaxGCPauseMillis=50 
-XX:GCPauseIntervalMillis=200 
-XX:SurvivorRatio=4 
-XX:TargetSurvivorRatio=16 
-XX:MaxTenuringThreshold=4 
-XX:+UseAdaptiveGCBoundary 
-XX:-UseGCOverheadLimit 
-XX:+PrintGCDetails
-XX:+PrintGCDateStamps 
-XX:+UseGCLogFileRotation 
-XX:NumberOfGCLogFiles=5 
-XX:GCLogFileSize=10M 
-Xloggc:$GC_FILE_NAME 
-Xnoclassgc 
-XX:ErrorFile=$PREFIX/log/java_error%p.log 
-XX:+HeapDumpOnOutOfMemoryError 
-Dfile.encoding=UTF-8