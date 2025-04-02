# TheHive deployment with High Availability in Google Cloud Platform
This project demonstrates the deployment of high-availability, containerized instances of TheHive — an open-source incident response platform — across multiple Google Cloud Platform (GCP) virtual machines.

## The infrastructure includes:

🐳 Two Dockerized instances of TheHive, deployed on separate GCP VMs

🔃 An NGINX load balancer container to distribute incoming traffic

🪣 A centralized PostgreSQL database and Elasticsearch instance for structured data and fast search, also containerized

💾 Linux Logical Volume Manager (LVM) used for persistent storage of database and search engine data

⚙️ Automation scripts to avoid manual orchestration and promote infrastructure-as-code best practices

🔐 Secrets managed securely via environment variables

This deployment provides horizontal scalability, failover tolerance, and persistent storage in a multi-tiered architecture — suitable for real-world cybersecurity operations labs or student infrastructure projects.

## Links:

WEBAPP: https://hub.docker.com/r/thehiveproject/thehive

WEBAPP DEPENDENCY: https://hub.docker.com/_/elasticsearch

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
    |  TheHive 1  | (Docker)                      |  TheHive 2  | (Docker)
    | (Machine 1) |                               | (Machine 2) |
    +------+------+                               +------+------+
                    \                            /        
                     v------------+  +----------v           
                                  |  |                       
                                  |  |
    +-----------------------------+--+--------------------------+                       
    |       PostgreSQL (Docker) + Elasticsearch (Docker)        |
    |		      (Machine 4)                           |
    +-----------------------------------------------------------+
