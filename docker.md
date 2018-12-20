## Docker Architecture

## Docker Engine

### Container Related Commands
    $ docker [CMD][OPTS] CONTAINER
    
**Examples:**
    All examples provided here work in RHEL
    
**1. Run a container in interactive mode:**
     
    $ docker run -it rhel7/rhel bash                  # Run a bash shell inside an image
    [root@...../]# cat /etc/redhat-release            # Check the release inside container
    
 **2. Run a container in detached mode:**
      
    $ docker run --name mywildfly -d -p 8080:8080 jboss/wildfly
      
**3. Run a detached container in a previously created docker network:**
      
    $ docker network create mynetwork
    $ docker run --name mywildfly-net -d --net mynetwork -p 8080:8080 jboss/wildfly
      
**4. Run a detached container mounting a local folder inside the container:**
  
    $ docker run --name mywildfly-volume -d -v myfolder/:/opt/jboss/wildfly/standalone/deployments/ -p 8080:8080 jboss/windfly
      
**5. Follow the logs of a specific container:**
      
    $ docker logs -f mywildfly
    $ docker logs -f <container-name>
      
**6. List containers:**
      
    $ docker ps                                     # List only active containers
    $ docker ps -a                                  # List all containers
      
**7. Stop a container:**
     
    $ docker stop <container-name>                  # Stop a container
    $ docker stop -t 1 <container-name>             # Stop a container (timeout = 1 second)
      
**8. Remove a container:**
  
    $ docker rm <container-name>                    # Remove a stopped container
    $ docker rm -f <container-name>                 # Remove a stopped container. Force stop if it is active
    $ docker rm -f $(docker ps -aq)                 # Remove all containers
    $ docker rm $(docker ps -q -f "status=exited")  # Remove all stopeed containers
    
**9. Execute a new process in an existing container :**
    
    $ docker exec -it mywildfly bash               # Executes and access bash inside a WildFly container
    $ docker exec -it <container-name> <process>
       
--------------------------------------------------------------------------------------------------------------------------------|      
daemon        | Run the persistent process that manages containers                                                              
--------------------------------------------------------------------------------------------------------------------------------| 
attach        | Attach a running container to view its ongoing output or to control it interactively
--------------------------------------------------------------------------------------------------------------------------------|
commit        | Create a new image from a container’s changes
--------------------------------------------------------------------------------------------------------------------------------|
cp            | Copy files/folders between a container and the local filesystem
--------------------------------------------------------------------------------------------------------------------------------|
create        | Create a new container
--------------------------------------------------------------------------------------------------------------------------------|
diff          | Inspect changes on a container’s filesystem
--------------------------------------------------------------------------------------------------------------------------------|
exec          | Run a command in a running container
--------------------------------------------------------------------------------------------------------------------------------|
export        | Export the contents of a container’s filesystem as a ‘.tar’ archive
--------------------------------------------------------------------------------------------------------------------------------|
kill          | Kill a running container using SIGKILL or a specified signal
--------------------------------------------------------------------------------------------------------------------------------|
logs          | Fetch the logs of a container
--------------------------------------------------------------------------------------------------------------------------------|
pause         | Pause all processes within a container
--------------------------------------------------------------------------------------------------------------------------------|
port          | List portmappings, or lookup the publicfacing port that is NATed to the PRIVATE_PORT
--------------------------------------------------------------------------------------------------------------------------------|
ps            | List all containers
--------------------------------------------------------------------------------------------------------------------------------|
rename        | Rename a container
--------------------------------------------------------------------------------------------------------------------------------|
restart       | Restart a container
--------------------------------------------------------------------------------------------------------------------------------|
rm            | Remove/delete one or more containers
--------------------------------------------------------------------------------------------------------------------------------|
run           | Run a command in a new container
--------------------------------------------------------------------------------------------------------------------------------|
start         | Start one or more containers
--------------------------------------------------------------------------------------------------------------------------------|
stop          | Stop a container by sending SIGTERM then SIGKILL after a grace period
--------------------------------------------------------------------------------------------------------------------------------|
top           | Display the running processes of a container
--------------------------------------------------------------------------------------------------------------------------------|
unpause       | Unpause all processes within a container
--------------------------------------------------------------------------------------------------------------------------------|
update        | Update configuration of one or more containers
--------------------------------------------------------------------------------------------------------------------------------|
wait          | Block until a container stops, then print its exit code
--------------------------------------------------------------------------------------------------------------------------------|

