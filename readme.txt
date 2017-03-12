Install and fire up the Sandbox using the instructions here: http://maprdocs.mapr.com/home/SandboxHadoop/c_sandbox_overview.html. 

Use an SSH client such as Putty (Windows) or Terminal (Mac) to login. See below for an example:
use userid: user01 and password: mapr.

For VMWare use:  $ ssh user01@ipaddress 

For Virtualbox use:  $ ssh user01@127.0.0.1 -p 2222 

You can build this project with Maven using IDEs like Eclipse or NetBeans, and then copy the JAR file to your MapR Sandbox, or you can install Maven on your sandbox and build from the Linux command line, 
for more information on maven, eclipse or netbeans use google search. 

After building the project on your laptop, you can use scp to copy your JAR file from the project target folder to the MapR Sandbox:

use userid: user01 and password: mapr.
For VMWare use:  $ scp  nameoffile.jar  user01@ipaddress:/user/user01/. 

For Virtualbox use:  $ scp -P 2222 nameoffile.jar  user01@127.0.0.1:/user/user01/.  

Copy the data file from the project data folder to the sandbox using scp to this directory /user/user01/data/ekg.csv on the sandbox:

For Virtualbox use:  $ scp -P 2222 data/ekg.csv  user01@127.0.0.1:/user/user01/data/. 


Step 0: Create the topics to read from (ekgs) and write to (ekgp)  in MapR streams:

maprcli stream create -path /user/user01/stream -produceperm p -consumeperm p -topicperm p
maprcli stream topic create -path /user/user01/stream -topic ekg -partitions 1
maprcli stream topic create -path /user/user01/stream -topic ekgp -partitions 1

to get info on the ekgs topic :
maprcli stream topic info -path /user/user01/stream -topic ekg

to delete
maprcli stream topic delete -path /user/user01/stream -topic ekgp 
____________________________________________________________________

Edit  "application.properties" by  replacing with destination environment variables. 
Run the below command at the project directory "/user/user01/live-mapr-streaming-websocket/" to execute the jar with overridden configuration file 
$ java -jar live-mapr-streaming-websocket-0.1.jar --spring.config.location=/user/user01/application.properties
Open the browser and browse the url -  http://servername:8070/ 




