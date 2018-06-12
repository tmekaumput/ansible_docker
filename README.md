# Ansible + Docker

This probject is a series of experiments in Ansible Docker plugins for sharing with community and also to keep track of my own journey!!!


# Get Ready!

  - Register myself to DockerHub
  - Getting Docker setup
  - Installing python-pip module
  - Import docker-py
  - Getting DNS server set up

# Get Started!

### Setting up inventory file
As DNS server has been set up, my initial inventory file is set up with docker.iomate.local host.
These following variables also added to group_vars/all for docker login command.

  - docker_hub_user
  - docker_hub_password
  - docker_hub_email
  
Docker login

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
