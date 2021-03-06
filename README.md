# Ansible + Docker

This probject is a series of experiments in Ansible Docker plugins for sharing with community and also to keep track of my own journey!!!


# Get Ready!

  - Getting Docker setup
  - Installing python-pip module
  - Import docker-py

# Get Started!

### Setting up inventory file
As DNS server has been set up, my initial inventory file is set up with docker.iomate.local host.
These following variables also added to group_vars/all for docker login command.

  - docker_hub_user
  - docker_hub_password
  - docker_hub_email

#### Ansible + Docker login

  - Creating docker_login.yml
  - Make sure it works by running command 
    
        $ansible-playbook docker_login.yml
    
  - Happy with the result below

        PLAY [docker.iomate.local] *********************************************************************************************
        TASK [Gathering Facts] *************************************************************************************************
        ok: [docker.iomate.local]
        TASK [Login to DockerHub] **********************************************************************************************
        changed: [docker.iomate.local]
        TASK [Logout from DockerHub] *******************************************************************************************
        ok: [docker.iomate.local]
        PLAY RECAP *************************************************************************************************************
        docker.iomate.local        : ok=3    changed=1    unreachable=0    failed=0

#### Ansible + Docker Container and Image

Ansible provides docker_image module to deal with Docker images and docker_container module to execute docker commands on the container. It allows us to perform basic operations such as start and stop container, removing container, as well as more complex task such as network set up, CPU/memory/storage allocation. This is a first baby step to play with image and container via the modules.

  - Create docker_container_image.yml
  - Make sure it works by running command 
    
        $ansible-playbook docker_container_image.yml

#### Ansible + Docker Network Basic

There you go!!! The docker_network module accommodates Docker network configuration. It supports custom networks as you would often need to set up containers in multiple zones such as proxy frontend, application server, and backend data tier, and more. 

    $ansible-playbook docker_network.yml

### Ansible + Docker Volume

In real world, applications are often redeployed with changes, and fixes without need to refresh persistent data.
Developer may just want to refresh new version of the application with minor change, or tester will need to get updated version of the application deployed to run test on existing test data already pre-loaded. 
The docker_container module supports volumes parameter to allow Docker to control and manage volumes of the container.
It also comes with docker_volume module to manage volumes specifically.

    $ansible-playbook docker_volume.yml

### Ansible + Docker Compose

Fundamentally Docker Compose is a blueprint yaml file that feeds into docker-compose binary that talks to Docker API to manage images and containers defined in the compose file, so we have to have the Docker Daemon running.
Ansible got this covered by using docker_service module, unfortunately the module supports compose file upto version 2 only as per statement in the document.

The module supports external compose file using **project_src** or using **definition** for an embed docker compose content in Ansible playbook.

**NOTE**: It requires docker-compose python library, getting it installed with the command below

    pip install docker-compose

**NOTE**: It may require to remove docker-py module depends on initial setup of the host that runs docker. Remove both docker and docker-py, then re-install only docker module will solve the problem.

    pip uninstall docker-py
    pip uninstall docker
    pip install docker