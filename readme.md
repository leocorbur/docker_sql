# PostgreSQL Data Ingestion with Docker

This repository aims to facilitate data ingestion into PostgreSQL using Docker. Follow these steps to set it up on your computer:

## Prerequisites

First, ensure that you have **Docker** installed. You can install it via the terminal or by using Docker Desktop. Docker Desktop provides a graphical interface for managing your Docker images and containers, which can be helpful.

Next, clone this repository to your computer either by downloading it directly or using the following terminal command:

 ``` bash
 git clone https://github.com/leocorbur/docker_sql.git
 ```

## Instructions  

### Create Folders

After cloning the repository to your computer, create two folders within the project directory and name them as follows:

- `data_pgadmin` 
- `ny_taxi_postgres_data` 

These folders are meant to **persist** changes in your ingested data and configurations, regardless of how many times you delete your images or containers.

### Build the Python Image

Before building the Python image, navigate to the main folder in your terminal as Docker needs to locate your **Dockerfile**. Then, execute the following command:

``` bash
docker build -t taxi_ingest:v001 .
```

If you're using Docker Desktop, you will see the Python image created in the images section.

### Run Docker Compose

To start the Docker Compose, ensure your terminal is in the main folder and execute the following command:

``` bash
docker-compose up
```

You'll observe two images created and two containers created within a default network, typically named *docker_sql_default*. You can view the network name by executing the command `docker network ls` in your terminal.

With Docker Compose running, open your browser and navigate to `localhost:8080`, to access **pgAdmin**. Use the following credentials to log in:
- Email: admin@admin.com
- Password: root

After logging in, register or create a server with the following connections:
- Hostname/address: pgdatabase
- Port: 5432
- Username: root
- Pass: root

### Ingest Data into PostgreSQL

There are two methods for ingesting data into PostgreSQL. 

1. Utilizing a Python script named `ingest_data.py`. To run this script, establish a connection with the containers by executing the following command in your terminal:

```bash
URL="https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/yellow_tripdata_2021-01.csv.gz"

docker run -it \
    --network=docker_sql_default \
    taxi_ingest:v001 \
    --user=root \
    --password=root \
    --host=pgdatabase \
    --port=5432 \
    --db=ny_taxi \
    --table_name=yellow_taxi_trips \
    --url="${URL}"
```

Note that you can practice with different datasets by modifying the script.

2. Utilizing the `upload_data.ipynb` notebook for a more personalized approach. Check the provided sample inside and try it with different datasets. Ensure to install the required libraries such as pandas, sqlalchemy, psycopg2, depending on your dataset.

Once you have ingested the data, you can run SQL queries in PostgreSQL without installing any additional software on your computer, only using Docker.


## Contribute

Feel free to contribute!

Contributor: Leonel Cortez

Email: leocorbur@gmail.com










