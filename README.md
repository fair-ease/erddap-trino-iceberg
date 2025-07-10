# ERDDAP, Trino and Iceberg Integration demo
This repository demonstrates configuring ERDDAP to talk to Trino usign the the Trino jdbc driver and thus enable ERDDAP to access an Apache Iceberg Data Lake House via the Trino Query Engine


The demo is based on the [Apache Iceberg Spark Quickstart](https://iceberg.apache.org/spark-quickstart/) docker compose file 

The "Apache Iceberg Quick start" consists of:
- A Minio object store container
- A Minio helper container that creates the Data Lakehouse S3 bucket
- A pyspark enabled Jupyter lab environment 
- A container running an Apache Iceberg REST catalog

For this demo the compose file has been edited to add:
- A Trino container to show how a Trino Query engine can be connected to the Apache Iceberg Lakehouse
- Setup files for configuring the Trino container with a java keystore
- An ERDDAP Instance and associated Trino JDBC jar file and ERDDAP configuration files and folders


## Setup

```console
git clone https://github.com/fair-ease/erddap-trino-iceberg
cd erddap-trino-iceberg
docker compose pull
docker compose up
```

This will bring up Minio, pyspark jupyter, iceberg rest, Trino and ERDDAP containers

Wait until all the containers appear to be up and running. 

Then browse to the pyspark jupyter notebook
http://localhost:8888/notebooks/notebooks/Glodap_iceberg.ipynb 

Run the first 5 cells in the notebook, this will load Glodap data from a parquet file into an iceberg lakehouse (stored on Minio S3 container)

Then stop the erddap container 

```console
docker compose stop erddap
```
Then restart it 
```console
docker compose start erddap
```
Browse to the erddap instance, you should see data set here:

                http://localhost:8095/erddap/tabledap/glodap_v2_2023_iceberg2.graph

Trino monitoring should be visible here:

                http://localhost:8090


