# Overview
This project involved the containerization and deployment of a full-stack yolo application using Docker.


# Requirements
Install the docker engine here:
- [Docker](https://docs.docker.com/engine/install/) 

## How to launch the application 
### Method 1 (faster)
- NOTE: This method does not require cloning of this repository

- Navigate to the launch_app folder and copy the contents of the [docker-compose.yaml] in the root of the project
- On your local machine, navigate to your desired directory and create
  a docker-compose.yaml file, paste the contents into it and save

  `touch docker-compose.yaml`

- Launch the application using docker compose up

  `docker compose up`

### Method 2
- NOTE: This requires cloning of this whole repository

- Clone this repository to your local machine

  `git clone https://github.com/brianbwire5/yolo.git`

- Navigate to the root directory of your cloned repository

  `cd yolo`

- Launch the application using the docker compose command

  `docker compose up`

## Access the application on your browser using the following URL
 `http://localhost:3000/`

## How to stop the application
- Navigate back to your terminal and press "ctrl+c" 

## How to terminate the application completely
 `docker compose down`

## The Docker images used in this application are sourced from this repository

https://hub.docker.com/repositories/nyagaah

![Alt text](nyagaah/yolo_app:1.0)

## How to run the app
Use vagrant up --provison command 
Ansible Playbook for [Project Name]
Overview
This Ansible playbook is designed to [ "configure a web server" and "deploy a database cluster"]. It uses Ansible's automation capabilities to simplify the process of setting up and managing [related infrastructure or applications].

Requirements
Ansible 2.9 or later
Python 3.8 or later
[List any other dependencies or requirements, e.g., specific Linux distributions or software packages]
Inventory File
The playbook uses an inventory file to define the hosts and groups that will be targeted by the playbook. The inventory file is located in the same directory as this README file and is named inventory.

Playbook File
The playbook file is named playbook.yml and is located in the same directory as this README file.

Usage
To run the playbook, navigate to the directory containing the playbook file and inventory file, and run the following command:


Verify

Open In Editor
Edit
Copy code
ansible-playbook -i inventory playbook.yml
This will execute the playbook against the hosts defined in the inventory file.

Variables
The playbook uses several variables that can be customized to suit your specific needs. These variables are defined in the group_vars and host_vars directories.

Roles
The playbook uses several roles to organize the tasks and handlers. These roles are located in the roles directory.


