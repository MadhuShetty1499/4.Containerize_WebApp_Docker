# Project-4: Containerize_WebApp_Docker
Containerization of Multi-Tier Java Application using Docker.

### Scenario:
  - Multi-Tier Application stack.
  - Running on VM's.
  - Regular deployment.
  - Continuous changes.

### Problem:
  - High CapEx and OpEx.
  - Human errors in deployment.
  - Not compatible with microservice architecture.
  - Resource wastage.
  - Not portable, Environment is not in sync.

### Solution:
  - Containers.
  - Consumes low resources.
  - Suits very well for microservice design.
  - Deployment via images.
  - Same container images across an environment.
  - Reusable and repeatable.

### Prerequisite:
  1. Oracle VM Virtualbox.
  2. Vagrant.
  3. Git bash or equivalent editor.
  4. Visual studio.
  5. Dockerhub account.

  Note - I have used Vagrant VM instead of EC2. It's up to you to choose any of them.

### Application Stack Architecture
![Architecture](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/images/architecture.png)

  - Tomcat: Serves as the webserver to host the Java-based application.
  - MySQL: A relational database for storing user data securely.
  - Nginx: Acts as a load balancer to distribute traffic across multiple application instances.
  - Memcached: Provides caching capabilities for improved performance.
  - RabbitMQ: Used for queuing and messaging between various application components.

### Detailed Steps:
  #### Setting up VM:
  - Create a new folder on your local computer.
  - Copy the Ubuntu 22 vagrant box from -[Vagrant Cloud](https://app.vagrantup.com/boxes/search).
  - Open git bash and get into the created folder.
  - Initialize vagrant VM. $`vagrant init bento/ubuntu-22.04`
  - Edit Vagrant file. $`vim Vagrantfile`
  - Change private ip address for your convenience and also uncomment public ip as shown.
  - Also, change the RAM size to 2048 for better speed, save the file and close.
    ![Vagrantfile](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/images/vagrantfile.png)
    
  - Bring up VM. $`vagrant up`
  - Login to VM. $`vagrant ssh` (Password='vagrant' if asked)
  - Switch to root user and install docker engine on ubuntu from official documentation - [Docker](https://docs.docker.com/engine/install/ubuntu/).
  - Add vagrant user to docker group to run docker commands without sudo privileges. $`usermod -aG docker vagrant`
  - Exit from VM and login again and verify docker commands running for vagrant user.
    ![Docker](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/images/docker.png)

  #### Dockerhub and Dockerfile references:
  - Go to https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker.git, switch to containers branch, fork it to your account and clone it to local where vagrant file is present (new folder).
  - Create three repositories in Dockerhub (vprofileapp, vprofileweb, vprofiledb).

  #### Dockerfile for App image:
  - Go to VS code => open cloned repo folder => dockerfiles => app => open Dockerfile => write the docker file as in [App](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/dockerfiles/app/Dockerfile) 

  #### Dockerfile for DB image:
  - Go to VS code => open cloned repo folder => dockerfiles => db => open Dockerfile => write the docker file as in [DB](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/dockerfiles/db/Dockerfile)

  #### Dockerfile for Web image:
  - Go to VS code => open cloned repo folder => dockerfiles => web => open Dockerfile => write the docker file as in [Web].(https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/dockerfiles/web/Dockerfile)
  - Also create custom configuration file (nginvproapp.conf) for nginx alongside it's Dockerfile as in [Configuration](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/dockerfiles/web/nginvproapp.conf).

  #### Docker compose:
  - Go to VS code => open cloned repo folder => create docker-compose.yml file => write the docker file as in [Docker-compose](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/docker-compose.yml)

  #### Build and Run:
  - Reboot the VM. $`vagrant reload`
  - Login to VM => cd to vagrant folder $`cd /vagrant/` => check dockerfiles and docker compose file in that folder.
  - Build the docker images $`docker compose build` => check images after build $`docker images`
  - Run the containers. $`docker compose up -d` => check the container running $`docker ps`
    ![Images](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/images/images.png)

  #### Validation
  - Copy the private Ip of VM which was set initially and paste it into the browser.
  - Login as admin_vp (username and password both) and check the services.
    ![WebApp](https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker/blob/main/images/login.png)

  #### Cleanup
  - Login to docker account in the VM $`docker login` and enter the username and password of dockerhub.
  - Upload the images to docker hub account $`docker push <image_name>` (all three images).
  - Stop the containers $`docker compose down`.
  - Delete all the stopped containers, unused images and networks $`docker system prune -a`.
  - Push all the dockerfiles and compose file to github.
  - Exit from the VM and terminate the VM $`vagrant destroy`.

### Credits
  - https://github.com/devopshydclub/vprofile-project

