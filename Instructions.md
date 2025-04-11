# 1. Start up for multiple docker compose files

### a. Order that things need to start up
1. Database
2. App 1    # Need to make an account first before starting App 2
3. App 2    # Need to have App 1 and App 2 up before starting the load balancer
4. Load Balancer 

### b. docker compose file start up order
1. `docker-compose -f docker-compose-db.yml up -d`
2. `docker-compose -f docker-compose-app-1.yml up -d`
3. `docker-compose -f docker-compose-app-2.yml up -d`
4. `docker-compose -f docker-compose-lb.yml up -d`

### c. Shutdown the containers
1. `docker-compose -f docker-compose-lb.yml down -v`
2. `docker-compose -f docker-compose-app-2.yml down -v`
3. `docker-compose -f docker-compose-app-1.yml down -v`
4. `docker-compose -f docker-compose-db.yml down -v`

# 2. Start Up for single docker compose file

### a. Order that things need to start up
1. Database
2. App 1    # Need to make an account first before starting App 2
3. App 2    # Need to have App 1 and App 2 up before starting the load balancer
4. Load Balancer 

### b. Starts database and app-1. Configure the admin account via app-1 IP:PORT
`docker compose up -d wikijs-db wikijs-app-1`

### c. Start app-2 and the load balancer. This allows app-2 too sync with the account app-1 made and allows the load balancer to work. Access via load balancer IP:8080
`docker compose up -d wikijs-app-2 wikijs-lb`

### d. Shutdown the containers
`docker-compose down -v`

# 3. To interact with the database directly
### Install one of these Tools:

#### GUI Tools:
    PGadmin
    DBeaver

#### CLI Tools:
    psql
        psql -h localhost -p 5432 -U wikiuser -d wiki

# 4. Good Postgre CheatSheet
https://quickref.me/postgres.html