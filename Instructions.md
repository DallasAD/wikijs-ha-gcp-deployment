# Start Up

## Starts database and app-1..
## Configure the admin account via app-1 IP:PORT
docker compose up -d wikijs-db wikijs-app-1

## Start app-2 and the load balancer
## This allows app-2 too sync with the account app-1 made and allows the load balancer to work. Access via load balancer IP:8080
docker compose up -d wikijs-app-2 wikijs-lb

# To interact with the database directly
Install one of these GUI Tools:
    PGadmin
    DBeaver

CLI tools:
    psql
        psql -h localhost -p 5432 -U wikiuser -d wiki

# Good Postgre CheatSheet
https://quickref.me/postgres.html