# Docker_by_Ayushi
What is a container ?
A container is a lightweight, standalone, and executable package of software that includes everything needed to run an application- code, runtime, system tools, libraries and settings.
container ensure that the application runs consitently regardless of the enviroment- whether on a developer's laptop, in a testing enviroment or in production.
![image](https://github.com/user-attachments/assets/1969cc8a-5aad-43be-8da9-363b321ce35d)

Why are containers light weight ?
Containers are light weight because they share the host system's operating system kernel instead of requiring their own OS like virtual Machine.
1.No Separte OS-unlike VM's conatiners don't bundle a full operating system. they use host OSkernel, which reduces overhead.
2.Faster startup-since there's is no OS to boot, conatiners can start in sec or milliseconds.
3.Lower resource usage- container use less CPU, memory, and storage compared to VM'sbecause they only include the app and its dependencies.
4.Smaller image sizes-Conatiner images are MB's in size, while VMimages are usually GB's.

Files and Folders in containers base images

/bin: contains commands such as ls , cp, ps
/sbin : system internal work commands like init
/lib : conatins library requied to run binaries
/usr : contains user- related files and utilities such as applications, libraries, and documentation.
/var: conatins changing data like logs, cache store here.
/tmp : temp files which are used for short duration.
/root : Root user home directory.
/proc, /sys, /dev : system hardware and kernel virtual files  

Files and Folders that containers use from host operating system
1. Host Kernel (Very Important)
• Containers always share the host’s Linux kernel which make conatiner light weight
• Kernel handles: process scheduling, memory mgmt, networking, etc.
2. Mounted Volumes (Optional)
When you manually mount host folders into containers (e.g. using -v or --mount), then containers can access host files/folders. using -docker run -v /host/folder:/container/folder my-image
•	Here, /host/path is a real folder on your host OS.
•	/container/path is where it appears inside the container.
•	This is used for:
•	Sharing config files, Persisting data,	Log file
3. Device Files (if passed)
If you pass specific device files like /dev/sda, the container can access host hardware. But this is rare and for advanced use cases (like Docker-in-Docker or storage apps
4. Network & IPC Namespaces (Shared or Isolated)
By default, containers have their own network namespace.
•	But you can share host’s network using:
docker run --network host my-image

What is Docker: Docker is a open source platform which packs the application into lightweight and portable conatiners which can ship run deploy on any platform withour worring about the enviroment
Earlier, we used to face the 'it works on my machine' problem. code would run on dev system but fail in prod due to enviroment mismatch.
sol'n -Docker - Docker solves this by putting the application, it libraries, dependencies and even enviroment configuration into one container image 


Docker Architecture :
1. Docker client (docker CLI): when u use commands like docker run, docker build, docker ps etc. client sends the request to docker daemon. it is the interface between to interact with docker.
2. Docker Daemon (dockerd) : its a background service and manages running container, building images, Network and volume on client request.
3. Docker Regirtry : A docker registry is for using docker images when you use docker pull or docker run commands the required images are pulled from the configured registry.
4. Docker file: Dockerfile is a file where you provide the steps to build your Docker images.

Practical
Day 1 : 
step1 install docker
       docker --version
     images:
       docker images (list docker images)
       docker pull <image_name> (pull image from Docker hub)
       docker build -t <image_name>:<tag> (build image from docker file)
       docker history <image_name> (history of an image)
       docker search <image_name> (search image on Docker hub)
     container:  
       docker run hello-world
       docker run -it ubuntu bash (-it for interactive +terminal , ubuntu -image , bash : command to run)
       docker run -d nginx (Run container in background)
       docker run --name 
       docker ps (list all running containers)
       docker ps -a (list all container with container id )
       docker run --name mycontainer ubuntu (run with name )
       docker run -d -p 8080:80 nginx ( run with port mapping )
       docker run -e MY_ENV=value ubuntu (run with env variable)
       socker start <container_id_or_name> (to start a container)
       docker stop <container_id_or_name>  (to stop a container)
       docker restart <container_id_or_name> ( to restart a container)
       docker rm <container_id> (to delete a container)
       docker rm $(docker ps -aq)
       docker rmi <image_id> or docker rmi ubuntu
       docker exec -it <container_id_or_name> ( Execute command inside container)
       docker attach <container_id> (To attach to an existing container)
       docker image prune -f ( delete the images which are not in use)
       docker inspect <container_id> (gives JSON details including ip address,volumes, mounts, config etc)
       docker logs <container_id>
       docker cp file.txt mera-container:/tmp/ (Host to container)
       docker cp mera-container:/tmp/file.txt ./ (container to Host)
       docker rename old_name new_name (container ka naam badalna)
       docker pause mera-container (container ko temporarily pause/unpause krna)
       docker port container_name (to check container ports)
       docker stats (container ke resource usage dekhna like CPU, RAM network usage)


Day2: Docker Volumes
  Advantages: 
  #Data persistence : even after container delete data is safe
  #Decoupling of data and container: Easy backup and restores.
  #shared volumes : ek volume ko multiple container use kr skate h
  #Performance : Docker volumes are optimized and better than bind mounts in most cases.  
      Docker volumes are preferred mechanism for persisting data generated and used by Docker container. (jab hum docker container chalate h wo apna data container ke file system ke ander store karta hai. lekin jaise hi container delete hota hai, uska pura data bhi 
      chala jata hai. is problem ko solve krne ke liye docker volumes use kiye jate hain yeh ek persistent storage provide krte hain. jo container ke life cycle se independent hota hai.
      Types of volume mounting 
      1. Named volume: docker khud manage krta hai 
      docker run -v myvol:app nginx
      2. Bind Mount: Tu host ka specific path deta hai
      docker run -v /home/user/data:/app nginx

      common commands 
      docker volume create my vol 
      docker volume ls
      docker volume inspect myvol
      docker volume rm myvol
      
       
      
       
       
       
       
