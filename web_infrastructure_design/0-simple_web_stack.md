# Simple Web Stack

## Overview

This document outlines the design of a single-server web infrastructure for hosting the website `www.foobar.com`. The setup includes a web server (Nginx), an application server, a database (MySQL), and a domain name configuration.

## Components

1. **Server**: The physical or virtual machine with IP `8.8.8.8` that hosts the web application and services.

2. **Domain Name**: `foobar.com` is a human-readable address configured with a `www` record pointing to the server’s IP address. This simplifies user access to the website.

3. **DNS Record**: The `www` subdomain in `www.foobar.com` is configured with a CNAME record pointing to the root domain or an A record pointing directly to `8.8.8.8`.

4. **Web Server (Nginx)**: Handles HTTP requests from users, serves static content, and forwards requests to the application server.

5. **Application Server**: Executes the web application code, processes requests, and communicates with the database to fetch or store data.

6. **Database (MySQL)**: Stores and manages data required by the application, handling queries from the application server.

7. **Communication**: The server communicates with user computers via HTTP/HTTPS protocols, facilitated by the web server (Nginx).

## Issues

1. **Single Point of Failure (SPOF)**: A single server means that if it fails, the entire website becomes inaccessible.

2. **Downtime During Maintenance**: Updating or deploying new code can lead to temporary downtime as the server needs to be restarted.

3. **Scalability Limitations**: The single server setup cannot efficiently handle high traffic loads, risking slowdowns or crashes under heavy traffic.