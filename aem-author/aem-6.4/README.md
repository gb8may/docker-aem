# About this aem-author-6.x
This is the repo of the docker image for AEM author. See the Docker [hub page](https://hub.docker.com/r/cheproximity/aem-author/) for the full readme on  how to use this Docker images.
This image includes AEM 6.x (author instance), Ubuntu 16.04 LTS and the Oracle JAVA 1.8(JRE).

## Setup to Run
1. Place the AEM JAR package to the current folder and rename it to `aem-author-4502.jar` as it's refference to the Dockerfile.
2. Updated the `license.properties` file with your AEM license details.
3. Run the following command to build the image:
`docker build -t <IMAGE-NAME> .`
4. Run the following command to run the created image:
`docker run -p 4502:4502 -it --name=<CONTAINER-NAME> -v ${PWD}/license.properties:/opt/aem/author/license.properties <IMAGE-NAME>  /bin/bash`


## Test AEM 6.4 server running

The `entrypoint.sh` shell script will be executed when docker container run and the AEM author instance is ready to go.

You would see the following console output when run the above ```docker run...``` command

```bash
$ docker run -p 4502:4502 -it -v ${PWD}/license.properties:/opt/aem/author/license.properties aem-author /bin/bash
Loading quickstart properties: default
Loading quickstart properties: instance
Low-memory action set to fork
Using 64bit VM settings, min.heap=1024MB, min permgen=256MB, default fork arguments=[-Xmx1024m, -XX:MaxPermSize=256m]
**** WARNING: insufficent heap memory ******************************************
The JVM reports 910 MB but we recommend at least 1024 MB +/- 20
Use your JVM's heap size option (like -Xmx1024M) to set that size.
Will fork a JVM to get enough memory.
********************************************************************************
Available memory below specified limits and low-memory action set to fork, will fork to get enough memory
Preparing to fork JVM, OS name=Linux, isWindows=false
Forking JVM: [/usr/lib/jvm/java-8-oracle/jre/bin/java, -Xmx1024m, -XX:MaxPermSize=256m, -jar, /opt/aem/author/aem-author-4502.jar, -nofork, -pt, CHILD, -nobrowser]
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=256m; support was removed in 8.0
Loading quickstart properties: default
Loading quickstart properties: instance
Low-memory action set to fork
Using 64bit VM settings, min.heap=1024MB, min permgen=256MB, default fork arguments=[-Xmx1024m, -XX:MaxPermSize=256m]
**** WARNING: insufficent heap memory ******************************************
The JVM reports 910 MB but we recommend at least 1024 MB +/- 20
Use your JVM's heap size option (like -Xmx1024M) to set that size.
Will fork a JVM to get enough memory.
********************************************************************************
Available memory below specified limits and low-memory action set to fork, will fork to get enough memory
Not forking JVM as -nofork option is set
Setting properties from filename '/opt/aem/author/aem-author-4502.jar'
Option '-quickstart.server.port' set to '4502' from filename aem-author-4502.jar
Verbose option not active, closing stdin and redirecting stdout and stderr
Redirecting stdout to /opt/aem/author/crx-quickstart/logs/stdout.log
Redirecting stderr to /opt/aem/author/crx-quickstart/logs/stderr.log
Press CTRL-C to shutdown the Quickstart server...
```

Just open the following URL in a browser window and wait for few minutes until AEM initialize the libraries. 
```
http://localhost:4502
```

### Register AEM instance
If the ```license.properties``` file is updated with details of AEM registration before container run, it would allow to login to the AEM. Othewise, it would prompt a window to enter details of the AEM registration.
