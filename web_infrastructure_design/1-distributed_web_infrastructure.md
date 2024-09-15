# Advanced Web Stack Design

## Overview

This document outlines a more advanced web infrastructure design with two servers, a load balancer, a web server, an application server, and a database. This setup improves upon a basic single-server design by adding redundancy and load distribution.

## Infrastructure Components

### 1. **Servers**
- **Definition**: Two physical or virtual machines are used to host the infrastructure components. These servers help in distributing the load and providing redundancy.

### 2. **Web Server (Nginx)**
- **Purpose**: Handles HTTP requests from users and serves static content. It also forwards requests to the application server if necessary.

### 3. **Application Server**
- **Purpose**: Runs the application code, processes business logic, and interacts with the database to handle dynamic content requests.

### 4. **Load Balancer (HAProxy)**
- **Purpose**: Distributes incoming traffic across multiple servers to ensure no single server becomes overwhelmed. This improves performance and availability.
  
- **Distribution Algorithm**: HAProxy can be configured with various algorithms, such as Round Robin, Least Connections, or IP Hash. Round Robin distributes requests evenly across servers. Least Connections routes traffic to the server with the fewest active connections, while IP Hash routes requests based on the client's IP address.

- **Active-Active vs. Active-Passive**:
  - **Active-Active**: All servers handle traffic simultaneously, improving resource utilization and balancing the load. 
  - **Active-Passive**: One server handles traffic while the other is on standby. If the active server fails, the passive server takes over. This setup reduces resource utilization but provides failover capabilities.

### 5. **Application Files**
- **Purpose**: The codebase for the web application is stored and managed on the application server. This includes scripts, templates, and other necessary files.

### 6. **Database (MySQL)**
- **Purpose**: Manages and stores application data. In a Primary-Replica (Master-Slave) setup:
  - **Primary Node**: Handles all write operations and updates to the database.
  - **Replica Nodes**: Handle read operations and provide data redundancy. Replicas are updated with changes from the primary node.

## How the Infrastructure Works

1. **User Requests**: A user sends an HTTP request to `www.foobar.com`.
2. **DNS Resolution**: The request is routed to the load balancer's IP address.
3. **Load Balancer (HAProxy)**: Distributes the request to one of the available servers based on the configured algorithm.
4. **Web Server (Nginx)**: Receives the request and serves static content or forwards it to the application server.
5. **Application Server**: Processes the request, executes application logic, and interacts with the database if necessary.
6. **Database (MySQL)**: The application server queries the database (primary or replica) to retrieve or store data.

## Issues and Considerations

### 1. **Single Points of Failure (SPOF)**
- **Potential SPOFs**:
  - **Load Balancer**: If HAProxy fails and there is no redundancy, the infrastructure could become inaccessible.
  - **Database Primary Node**: If the primary database node fails, write operations cannot be processed. 

### 2. **Security Issues**
- **No Firewall**: Lack of a firewall leaves the infrastructure vulnerable to attacks.
- **No HTTPS**: Without HTTPS, data transmitted between users and the server is not encrypted, risking data breaches.

### 3. **No Monitoring**
- **Issue**: Without monitoring tools, it's challenging to track performance, detect issues, and ensure the infrastructure operates smoothly.

## Conclusion

This advanced web stack design introduces redundancy and load balancing to improve performance and availability compared to a single-server setup. However, it is crucial to address potential issues such as SPOFs, security vulnerabilities, and lack of monitoring to ensure a robust and reliable infrastructure.
