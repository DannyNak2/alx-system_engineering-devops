# 0x09 - Web Infrastructure Design

This project contains whiteboard-designed web infrastructure diagrams and explanations for different system architectures, starting from a simple single-server setup to a secured, monitored, and scalable infrastructure.

---

## Table of Contents
- [Project Overview](#project-overview)
- [Tasks](#tasks)
  - [0. Simple Web Stack](#0-simple-web-stack)
  - [1. Distributed Web Infrastructure](#1-distributed-web-infrastructure)
  - [2. Secured and Monitored Web Infrastructure](#2-secured-and-monitored-web-infrastructure)
  - [3. Scale Up (Advanced)](#3-scale-up-advanced)
- [Repository Information](#repository-information)

---

## Project Overview
The goal of this project is to design and explain various web infrastructure setups, each progressively more robust, secure, and scalable.  
These designs are presented in a **whiteboard format** and accompanied by **detailed explanations** covering:
- Roles of each component in the infrastructure.
- Benefits of the chosen design.
- Potential single points of failure (SPOFs) and limitations.
- Security considerations.
- Scalability improvements.

---

## Tasks

### 0. Simple Web Stack
**Scenario**:  
A **single server** hosts a website reachable via `www.foobar.com` using a **LAMP-like** architecture with:
- 1 server  
- 1 web server (**Nginx**)  
- 1 application server  
- 1 set of application files (code base)  
- 1 database (**MySQL**)  
- 1 domain name with a `www` record pointing to server IP `8.8.8.8`.

**Key Points Explained**:
- Definition and purpose of a server.
- Role of the domain name and DNS record type (`A` record for `www`).
- Function of the web server, application server, and database.
- Communication between server and user (HTTP/HTTPS over TCP/IP).
- **Issues**:
  - SPOF (Single Point of Failure)
  - Downtime during maintenance (e.g., restarting Nginx during code deployment)
  - No scalability for high traffic

---

### 1. Distributed Web Infrastructure
**Scenario**:  
A **three-server** setup introducing load balancing and database replication:
- 1 load balancer (**HAProxy**)
- 1 web server (**Nginx**)
- 1 application server
- 1 primary database (**MySQL**) with **replica** node
- Shared application files

**Additional Elements Explained**:
- Load balancer distribution algorithms (e.g., round-robin).
- Active-Active vs Active-Passive configurations.
- Primary-Replica database replication:  
  - Primary node handles writes.
  - Replica node handles reads for load distribution.

**Issues**:
- SPOFs (load balancer or primary DB failure).
- Security risks (no firewall, no HTTPS).
- No monitoring in place.

---

### 2. Secured and Monitored Web Infrastructure
**Scenario**:  
A **three-server** setup with added security and monitoring:
- 3 firewalls (one per server)
- SSL certificate for `www.foobar.com` (HTTPS)
- 3 monitoring clients (e.g., Sumologic agents)

**Additional Elements Explained**:
- Role of firewalls in filtering traffic.
- Benefits of HTTPS (data encryption, integrity, authentication).
- Monitoring for uptime, QPS (queries per second), CPU/memory usage.
- Data collection by monitoring agents.

**Issues**:
- SSL termination at the load balancer can expose traffic internally.
- Single writable DB node limits fault tolerance.
- Identical servers with DB, web, and app server may cause resource contention.

---

### 3. Scale Up (Advanced)
**Scenario**:  
A **more scalable setup** with:
- Additional load balancer (HAProxy) in a **cluster** with the first one.
- Component separation into dedicated servers:
  - Web server on its own machine.
  - Application server on its own machine.
  - Database on its own machine.

**Additional Elements Explained**:
- Benefits of component separation (resource optimization, independent scaling).
- Increased fault tolerance with clustered load balancers.

---

## Repository Information
**GitHub Repository**: [alx-system_engineering-devops](https://github.com/DannyNak2/alx-system_engineering-devops)  
**Directory**: `0x09-web_infrastructure_design`  
**Files**:
- `0-simple_web_stack`
- `1-distributed_web_infrastructure`
- `2-secured_and_monitored_web_infrastructure`
- `3-scale_up`

---
