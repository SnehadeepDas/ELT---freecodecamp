# ELT---freecodecamp

https://www.youtube.com/watch?v=PHsC_t0j1dU&amp;t=3557s&amp;ab_channel=freeCodeCamp.org
Step 1: Docker Compose Configuration
docker-compose.yml File

Defines three services: source_postgres, destination_postgres, and elt_script.

Connects all services to the elt_network for inter-service communication.

Specifies environment variables, ports, volumes, and dependencies for each service.

Step 2: Building and Running Containers
source_postgres Service

Starts a PostgreSQL database container using the postgres:15 image.

Maps port 5432 in the container to port 5433 on the host.

Initializes the database with the init.sql script.

destination_postgres Service

Starts a PostgreSQL database container using the postgres:15 image.

Maps port 5432 in the container to port 5434 on the host.

elt_script Service

Builds a custom Docker image based on the provided Dockerfile.

Runs the elt_script.py script once source_postgres and destination_postgres are ready.

Step 3: Dockerfile Configuration
Dockerfile

Starts from the python:3.8-slim base image.

Installs PostgreSQL client tools using apt-get.

Copies the elt_script.py into the container.

Sets the default command to run the elt_script.py using Python.

Step 4: ELT Script Execution
elt_script.py

Imports and Functions:

Imports necessary modules (subprocess and time).

Defines a function wait_for_postgres to check PostgreSQL availability.

Main Execution:

Uses wait_for_postgres to ensure the source_postgres container is ready.

Defines configuration dictionaries for the source and destination PostgreSQL databases.

Uses pg_dump to create a dump of the source database and saves it as data_dump.sql.

Uses psql to load the data_dump.sql into the destination PostgreSQL database.

Prints start and end messages to indicate the script's progress.
