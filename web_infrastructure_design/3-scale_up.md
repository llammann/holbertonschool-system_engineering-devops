# Web Infrastructure Design

## Overview

This document describes a scalable web infrastructure with a focus on separating components across different servers and utilizing a load balancer for improved reliability and performance. It also explains the roles of application servers and web servers.

## Infrastructure Components

### 1. **Server**
- **Definition**: A physical or virtual machine that hosts the various components of the infrastructure.

### 2. **Load Balancer (HAProxy)**
- **Purpose**: Distributes incoming traffic across multiple servers to balance the load, improve performance, and ensure high availability.
- **Configuration**: Set up as a cluster with another load balancer to provide redundancy and fault tolerance.

### 3. **Web Server**
- **Purpose**: Handles HTTP requests from users and serves static content (e.g., HTML, CSS, JavaScript files).
- **Example**: Nginx or Apache.

### 4. **Application Server**
- **Purpose**: Executes application code and processes business logic. It interacts with the web server to handle dynamic requests and communicate with the database.
- **Example**: Node.js, Django, or Flask.

### 5. **Database (MySQL)**
- **Purpose**: Stores and manages application data. It handles queries, updates, and transactions.
- **Configuration**: Typically set up as a Primary-Replica (Master-Slave) cluster to ensure data redundancy and load distribution for read operations.

## Detailed Explanations

### **Server**
- **Role**: Hosts the infrastructure components. In a scalable design, each server handles a specific role to optimize performance and maintainability.

### **Load Balancer**
- **Why Add It?**: Distributes incoming traffic across multiple servers to avoid overload on any single server and enhance fault tolerance. By clustering load balancers, you ensure that if one fails, the other can continue to handle traffic.

### **Web Server vs. Application Server**
- **Web Server**:
  - **Role**: Manages HTTP requests and serves static content. It can also handle SSL termination and load balancing.
  - **Function**: Delivers files like HTML, CSS, and JavaScript directly to users’ browsers.
- **Application Server**:
  - **Role**: Processes dynamic content by executing application code. It handles business logic, user authentication, and interaction with the database.
  - **Function**: Generates dynamic content and interacts with the web server to deliver processed information to users.

### **Database (MySQL)**
- **Why Add It?**: Stores data required by the application. A Primary-Replica setup ensures high availability and improved read performance by offloading read queries to replica nodes.


## Conclusion

This infrastructure design ensures a scalable, reliable, and maintainable web application environment by clearly defining the roles of each component and using a load balancer to distribute traffic. Understanding the distinction between web servers and application servers helps in optimizing the handling of static and dynamic content, respectively.

For any additional questions or clarifications, please refer to the specific configuration details of each component.
