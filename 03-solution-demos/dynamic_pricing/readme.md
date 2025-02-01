# Dynamic Pricing Model

In this demo, we use RisingWave to dynamic pricing model. The data generators will generate purchase and restock events. Restock events happen at longer intervals. Data streams will be sent to a Kafka topic and static data on product information are stored in a Postgres database. We will use RisingWave to ingest and join Kafka and Postgres data to create a pricing model that adjust the sales price of products based on the demand.

## Prerequisites

Ensure you have the following installed:

- **[Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/install/):** Docker Compose is included with Docker Desktop for Windows and macOS. Ensure Docker Desktop is running if you're using it.
- **[PostgreSQL interactive terminal (psql)](https://www.postgresql.org/download/):** This will allow you to connect to RisingWave for stream management and queries.

## Launch the Demo Cluster

1. **Clone the Repository:** First, clone the [awesome-stream-processing](https://github.com/risingwavelabs/awesome-stream-processing) repository.
    
    ```bash
    git clone <https://github.com/risingwavelabs/awesome-stream-processing.git>
    
    ```
    
2. **Start the Demo Cluster:** Navigate to the `04-solution-demos/dynamic_pricing` directory, and start the demo using Docker Compose.
    
    ```bash
    cd awesome-stream-processing/04-solution-demos/dynamic_pricing
    docker compose up -d
    
    ```
    
    This will initiate the standalone mode of RisingWave, a Kafka instance, Zookeeper, PostgreSQL, and a Grafana instance. 
    
    > Note: Kafka is exposed on `kafka:9092` for internal applications and on `localhost:29092` for local applications. The corresponding source topic is created automatically.
    > 
3. **Connect to RisingWave:** Use `psql` to manage data streams and analyze data via materialized views. 
    
    ```bash
    psql -h localhost -p 4566 -d dev -U root
    ```

    Once connected, run all queries included in the [create-source](/04-solution-demos/dynamic_pricing/create_source.md) and [create-mv](/04-solution-demos/dynamic_pricing/create_mv.md) files.
    
4. **Build a dashboard:**

    Open the Grafana instance at `http://localhost:3000` and navigate to the Grid Monitoring dashboard. For this demo, Grafana has been configured to automatically read data from RisingWave. If the graphs are not loading, refresh the queries.