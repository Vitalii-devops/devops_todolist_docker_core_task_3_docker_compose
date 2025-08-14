# How to run and stop containers with docker-compose
Prerequisites
Docker installed on your system.
Your project directory contains a valid docker-compose.yml and Dockerfiles.

1. Build Docker images and start all services defined in docker-compose.yml
docker-compose up -d 
The -d flag runs containers in detached (background) mode.
This command sets up the containers, networks, and volumes as specified.
2. Verify containers are running
docker-compose ps
You should see containers pythonapp and MySQL database listed as Up.


**Required Environment Variables and Configuration**
For MySQL service in docker-compose.yml environment section:
MYSQL_ROOT_PASSWORD — root user password for MySQL, required.

MYSQL_DATABASE — Name of the default database to create.

MYSQL_USER — Username for a new MySQL user with access to the database.

MYSQL_PASSWORD — Password for the above user.
These variables allow MySQL to initialize the database and user on container startup.


**Access the web application:**
Open a web browser and go to:
http://localhost:8080/
Expected Output:
You should see Django application's homepage.
No connection errors to the database should appear in logs.

Check logs for running containers:
docker-compose logs pythonapp
docker-compose logs mysql

**Verify data persistence:**
Add a Todo item within Django app.
Stop and remove containers with:

docker-compose down
Start containers again:

docker-compose up -d
Confirm that the added data persists by querying the database or viewing the app.



**Troubleshooting Tips:**

Django cannot connect to MySQL:
Verify the MySQL hostname in Django settings matches the service name in docker-compose.yml (usually mysql).
Check MySQL container logs for startup issues:
docker-compose logs mysql
Data does not persist after container restart
Ensure you are using a Docker volume for MySQL data storage and that volume is mapped correctly (e.g., db-data:/var/lib/mysql).
Verify volume creation:

docker volume ls
Inspect volume usage on the MySQL container:

docker inspect my-sql
Container restart loops or crashes:

Check logs for errors:

docker-compose logs pythonapp
Review Dockerfile ENTRYPOINT or command syntax for correctness.