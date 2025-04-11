# Wiki.js High Availability Deployment on GCP
This project demonstrates the deployment of high-availability, containerized instances of [Wiki.js](https://wiki.js.org/)—an open-source Wiki software—across multiple Google Cloud Platform (GCP) virtual machines.

## The infrastructure includes:

📚 Two Dockerized instances of Wiki.js, deployed on separate GCP VMs

🔃 An NGINX load balancer container to distribute incoming traffic

🪣 A centralized PostgreSQL database

💾 Linux Logical Volume Manager (LVM) used for persistent storage of database data

⚙️ Automation scripts to avoid manual orchestration and promote infrastructure-as-code best practices

🔐 Secrets managed securely via environment variables

This deployment provides horizontal scalability, failover tolerance, and persistent storage in a multi-tiered architecture — suitable for real-world cybersecurity operations labs or student infrastructure projects.

## Links:
<<<<<<< HEAD

WEBAPP: https://hub.docker.com/r/strangebee/thehive/

WEBAPP DEPENDENCY: https://hub.docker.com/_/elasticsearch
=======
WIKI.JS: https://hub.docker.com/r/requarks/wiki
>>>>>>> refs/remotes/origin/main

DATABASE: https://hub.docker.com/_/postgres

LOAD BALANCER: https://hub.docker.com/_/nginx


## Architecture Diagram:


                          +----------------+
                          |     Client     |
                          |    (Browser)   |
                          +--------+-------+
                                   |
                            +------+------+
                            |   NGINX LB  | (Docker)
			        | (Machine 3) |
                            +------+------+
                                   |
           +-----------------------+-----------------------+
           |                                               |
    +------+------+                               +--------+----+
    |  Wiki.js 1  | (Docker)                      |  Wiki.js 2  | (Docker)
    | (Machine 1) |                               | (Machine 2) |
    +------+------+                               +------+------+
                    \                            /        
                     v------------+  +----------v           
                                  |  |                       
                                  |  |
    +-----------------------------+--+--------------------------+                       
    |                     PostgreSQL (Docker)                   |
    |		           (Machine 4)                      |
    +-----------------------------------------------------------+
