# Docker
Docker Stuff

The forked repository containing all the other files:
https://github.com/Tina-Gh/udemy-docker-mastery

Docker Completion:
https://github.com/matt9ucci/DockerCompletion

<be>

# In Bash - cause obviously :D
abc

# Ol' Windows stuff :D

I'm using Docker Toolbox, and http://localhost isn't working. What's wrong?
Docker Toolbox uses a default IP of http://192.168.99.100 and doesn't support the localhost feature of Docker for Windows/Mac.

$(pwd) in Windows Is getting an error for bind-mounts: C:\Program Files\Docker Toolbox\docker.exe: invalid reference format.
PowerShell has a few minor differences in command format. This is a PowerShell thing, not a docker thing. When using the shell path shortcut "pwd":

For PowerShell use: ${pwd} 

For cmd.exe "Command Prompt use: %cd%

bash, sh, zsh, and Docker Toolbox Quickstart Terminal use: $(pwd) 

Note, if you have spaces in your path, you'll usually need to quote the whole path in the docker command.

There's another issue sometimes seen, where other apps can mess up your path: https://stackoverflow.com/questions/50608301/docker-mounted-volume-adds-c-to-end-of-windows-path-when-translating-from-linux

I hit Ctrl-C in Windows and The Container is Still Running
In Windows, there's a quirk with the built-in Powershell and Command Prompt terminals. They don't interpret ctrl-c the same way as Linux, Unix, and macOS. They won't shutdown the container, and you'll need to use docker stop commands. Sorry for the confusion.

PowerShell Tab Completion Isn't Working Or I Can't Find the Page in Docs
The posh-docker repo is no longer being maintained, but a new better one now exists at https://github.com/matt9ucci/DockerCompletion so give that a shot. Then please thank the author if it works for you so they keep it updated. Yay open source!

I'm using Docker Toolbox and bind-mounts aren't working (sharing files between Windows and docker with -v  )
Docker Toolbox requires your files be in your profile under c:\users\<username>\   before file sharing will work in Toolbox.

Bind for 0.0.0.0:80 failed: port is already allocated. -OR- port already in use -OR- permission denied.
This will happen if you are attempting to start a new container with a port that is already in-use on your machine. Remember in TCP/UDP, only one application/service can use a single IP+PORT at a time. This doesn’t change with containers when you use -p  to bind to the host IP+PORT.

First run docker container ls  to check if there are any containers using this port - if there are not; you likely have a non-Docker related application running on your machine that is using this port. Maybe IIS, maybe Apache, etc.

If you are on a Mac, you can check what is using port 80 with the command: lsof -i :80  

If you are on Windows, you can check what is using port 80 with: netstat  

Of course - if you don’t have a reason to specifically use the port that is throwing this error, simply run your container on another port. Remember, the syntax is <host port>:<container port>  , so binding to port 8888 on your host machine with a container that uses port 80, would look like: docker container run -p 8888:80 your_image  

How do I cleanup space (images etc.)?
Run prune commands https://www.udemy.com/docker-mastery/learn/v4/t/lecture/7407918?start=0

Bind Mount Won't Show Up In Container
This is usually a Docker for Windows issue, where you need to go into Docker Settings GUI (lower right icon) and uncheck the drive where your code is, then save, and then re-check that drive to re-apply the SMB file sharing permissions between the Linux VM and the Windows OS.

Starting container process caused "exec: \"ping\": executable file not found in $PATH": unknown
That error is telling you that ping is not available in the image you’re trying to run it from. Official images have changed over time and the official nginx default image (nginx:latest) no longer has ping in it by default.  Image nginx:alpine should still have ping installed (a few of my videos show utilities like ping that are no longer in those images).

If it's a debian-based image (the default nginx) then you can also use apt-get update && apt-get install -y iputils-ping   inside the container to install it.

Lastly, I keep a “bunch of troubleshooting and handy admin utilities” in an image here that you can run ping from: bretfisher/netshoot  

https://www.udemy.com/docker-mastery/learn/v4/questions/3751216

Starting mysql container and running ps causes "ps: command not found"
Like above, this is the container shell telling you the binary "ps" isn't in your path, and not installed in the container. Docker changed the mysql image after the video was recorded and removed the ps utility. You can add it back in using the apt package manager.

apt-get update && apt-get install procps

For more info: https://stackoverflow.com/questions/26982274/ps-command-doesnt-work-in-docker-container

How to run two container websites on a single port in Docker or Swarm services
This is a bit more advanced, but common for production Swarms. You'll need a "reverse proxy"

https://www.udemy.com/docker-mastery/learn/v4/questions/3931678

Error response from daemon: pull access denied.
Double and triple-check the spelling of the image you are pulling; if you are attempting to pull a publicly hosted image - this error will not occur, but if there is a typo and Docker can’t find the image - it will expect that it is a private image and ask you to login.

Also, there are times when the config.json file gets messed up, so try docker logout && docker login. If all that still causes the same issue, try removing ~/.docker/config.json  and then pull again.

Kubernetes vs. Swarm.
I have a dedicated lecture for this: 

https://www.udemy.com/course/docker-mastery/learn/lecture/15094976

Does this help with Docker Certified Associate?
Yes, but it’s not a study guide. Here’s the Lecture with info: https://www.udemy.com/docker-mastery/learn/v4/t/lecture/9485678?start=0

Ubuntu Container vs. Ubuntu OS, What's the Difference?
https://www.udemy.com/docker-mastery/learn/v4/questions/5390204

How to use volumes in Swarm for databases.
https://www.udemy.com/docker-mastery/learn/v4/questions/2675184

How do we do backups in docker?
https://www.udemy.com/docker-mastery/learn/v4/questions/2756448

Getting a shell in VM’s that run Docker
Workaround: https://www.udemy.com/docker-mastery/learn/v4/questions/3860412

docker run -it --rm --privileged --pid=host justincormack/nsenter1  

macOS https://www.bretfisher.com/docker-for-mac-commands-for-getting-into-local-docker-vm/

Docker for Windows https://www.bretfisher.com/getting-a-shell-in-the-docker-for-windows-vm/

Docker Toolbox docker-machine ssh default  

Windows firewalls preventing networking or bind mounts in containers
https://www.udemy.com/docker-mastery/learn/v4/questions/3258290

Anti-Virus Blocking file sharing in Windows
https://www.udemy.com/docker-mastery/learn/v4/questions/3442460

Are containers more secure than VM’s?
https://www.udemy.com/docker-mastery/learn/v4/questions/4020880

I have a network proxy and images won’t build
https://stackoverflow.com/questions/23111631/cannot-download-docker-images-behind-a-proxy/

Public vs. Private IP for Swarm advertise-addr and data-path-addr
https://www.udemy.com/docker-mastery/learn/v4/questions/3710518

Custom Docker Networks, macvlan and IP setting hardcoding
https://www.udemy.com/docker-mastery/learn/v4/questions/3706540
