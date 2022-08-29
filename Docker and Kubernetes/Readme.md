# Docker and Kubernetes:


<h3> Section 1: Dive into Docker!</h3>

What is Docker? Why use Docker? What is image? What is container?

<h3> Section 2: Manipulating Containers with the Docker Client</h3>
  
  <p>
    Example: Connecting to Redis 

    in the first terminal -> docker run redis

    in the second terminal -> docker ps -> grab the redis image container ID -> docker exec -it [the grabbed ID] redis-cli
  </p>
  
<h3> Section 3: Building Custom Images through Docker Server </h3>

<p>  
  Make the image 
  
  docker build .
  
  Run the docker image command 
</p>
