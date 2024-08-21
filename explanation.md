## 1. Choice of Base Image
 The base image used to build the containers is `node:16-alpine3.16`. It is derived from the Alpine Linux distribution, making it lightweight and compact. 
 Used 
 1. Client:`node:16-alpine3.16`
 2. Backend: `node:16-alpine3.16`
 3.Mongo : `mongo:6.0 `
       

## 2. Dockerfile directives used in the creation and running of each container.
 I used two Dockerfiles. One for the Client and the other one for the Backend.

**Client Dockerfile**

```
# Build stage
FROM node:16-alpine3.16 as build-stage

# Set the working directory inside the container
WORKDIR /client

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies and clears the npm cache and removes any temporary files
RUN npm install --only=production && \
    npm cache clean --force && \
    rm -rf /tmp/*

# Copy the rest of the application code
COPY . .

# Build the application and  remove development dependencies
RUN npm run build && \
    npm prune --production

# Production stage
FROM node:16-alpine3.16 as production-stage

WORKDIR /client

# Copy only the necessary files from the build stage
COPY --from=build-stage /client/build ./build
COPY --from=build-stage /client/public ./public
COPY --from=build-stage /client/src ./src
COPY --from=build-stage /client/package*.json ./

# Set the environment variable for the app
ENV NODE_ENV=production

# Expose the port used by the app
EXPOSE 3000

# Prune the node_modules directory to remove development dependencies and clears the npm cache and removes any temporary files


# Start the application
CMD ["npm", "start"]

```
**Backend Dockerfile**

```
# Set base image
FROM node:16-alpine3.16

# Set the working directory
WORKDIR /backend

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install dependencies and clears the npm cache and removes any temporary files
RUN npm install --only=production && \
    npm cache clean --force && \
    rm -rf /tmp/*

# Copy the rest of the application code
COPY . .

# Set the environment variable for the app
ENV NODE_ENV=production

# Expose the port used by the app
EXPOSE 5000

# Prune the node_modules directory to remove development dependencies and clears the npm cache and removes any temporary files
RUN npm prune --production && \
    npm cache clean --force && \
    rm -rf /tmp/*

# Start the application
CMD ["npm", "start"]

```

## 3. Docker Compose Networking
The (docker-compose.yml) defines the networking configuration for the project. It includes the allocation of application ports. The relevant sections are as follows:


```
services:
  backend:
    # ...
    ports:
      - "5000:5000"
    networks:
      - yolo-network

  client:
    # ...
    ports:
      - "3000:3000"
    networks:
      - yolo-network
  
  mongodb:
    # ...
    ports:
      - "27017:27017"
    networks:
      - yolo-network

networks:
  yolo-network:
    driver: bridge
```
In this configuration, the backend container is mapped to port 5000 of the host, the client container is mapped to port 3000 of the host, and mongodb container is mapped to port 27017 of the host. All containers are connected to the yolo-network bridge network.


## 4.  Docker Compose Volume Definition and Usage
The Docker Compose file includes volume definitions for MongoDB data storage. The relevant section is as follows:

yaml

```
volumes:
  mongodata:  # Define Docker volume for MongoDB data
    driver: local

```
This volume, mongodb_data, is designated for storing MongoDB data. It ensures that the data remains intact and is not lost even if the container is stopped or deleted.

## 5. Git Workflow to achieve the task

To achieve the task the following git workflow was used:

1. Fork the repository from the original repository.
2. Clone the repo: `git@github.com:Maubinyaachi/yolo-Microservice.git`
3. Create a .gitignore file to exclude unnecessary     files and directories from version control.
4. Added Dockerfile for the client to the repo:
`git add client/Dockerfile`
5. Add Dockerfile for the backend to the repo:
`git add backend/dockerfile`
6. Committed the changes:
`git commit -m "Added Dockerfiles"`
7. Added docker-compose file to the repo:
`git add docker-compose.yml`
8. Committed the changes:
`git commit -m "Added docker-compose file"`
9. Pushed the files to github:
`git push `
10. Built the client and backend images:
`docker compose build`
11. Pushed the built imags to docker registry:
`docker compose push`
12. Deployed the containers using docker compose:
`docker compose up`

13. Created explanation.md file and modified it as the commit messages in the repo will explain.
Overview
This project uses Ansible to automate the deployment of a web server on a remote host. The project includes a playbook, roles, and variables files that work together to configure and deploy a web server with a sample web application.

Components
Playbook
The playbook is the main entry point for the Ansible deployment. It defines the roles and tasks that will be executed on the remote host. The playbook file is named playbook.yml and is located in the root of the project directory.

Roles
The project includes three roles:

common: This role installs common dependencies and configures the system.
webserver: This role installs and configures the web server software.
deploy_app: This role deploys a sample web application.
Each role has its own directory and includes a tasks file that defines the tasks to be executed.

Variables
The project includes a group_vars directory that contains variables files for different environments (e.g., dev, stg, prod). These variables files define settings for the web server, sample web application, database, and system.

How it Works
Here's a high-level overview of how the project works:

The playbook is executed on the remote host using Ansible.
The playbook includes the common role, which installs common dependencies and configures the system.
The playbook includes the webserver role, which installs and configures the web server software.
The playbook includes the deploy_app role, which deploys a sample web application.
The roles use variables from the group_vars directory to customize the deployment.
The playbook executes the tasks defined in each role, using the variables to configure the web server and deploy the sample web application.
Benefits
This project provides several benefits, including:

Automation: Ansible automates the deployment of the web server and sample web application, reducing the risk of human error.
Consistency: The project ensures consistency across different environments (e.g., dev, stg, prod) by using variables files to customize the deployment.
Flexibility: The project allows for easy customization of the deployment by modifying the variables files or adding new roles and tasks.
Getting Started
To get started with this project, follow these steps:

Install Ansible on your local machine.
Clone the project repository to your local machine.
Create an inventory file that defines the remote host and its credentials.
Run the playbook using the ansible-playbook command, specifying the inventory file and playbook file.
Troubleshooting
If you encounter any issues while running the playbook, you can increase the verbosity of the output by adding the -vvv flag to the command. This will provide more detailed information about the tasks and handlers being executed.


