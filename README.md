# Elasticsearch & Kibana Docker Setup

This repository contains a simple Docker Compose configuration for running **Elasticsearch** and **Kibana** locally using Docker. 

## Requirements

- **Docker** (version 3.8 or higher)
- **Docker Compose**

## Services

1. **Elasticsearch**:
   - **Image**: `docker.elastic.co/elasticsearch/elasticsearch:8.7.0`
   - **Ports**: Exposed on `localhost:9200` (Default Elasticsearch port)
   - **Volumes**: The Elasticsearch data is stored in the `./esdata` directory on the host machine.
   - **Environment Variables**:
     - `discovery.type=single-node`: Runs Elasticsearch in a single-node mode.
     - `xpack.security.enabled=false`: Disables X-Pack security for easy setup.

2. **Kibana**:
   - **Image**: `docker.elastic.co/kibana/kibana:8.7.0`
   - **Ports**: Exposed on `localhost:5601` (Default Kibana port)
   - **Depends On**: Elasticsearch (Kibana will wait for Elasticsearch to be available before starting).
   - **Environment Variables**:
     - `ELASTICSEARCH_HOSTS=http://elasticsearch:9200`: Configures Kibana to connect to the Elasticsearch service.

## How to Run

1. Ensure that Docker is installed and running on your machine.
2. Clone the repository or download the `docker-compose.yml` file.
3. Navigate to the directory containing the `docker-compose.yml` file.
4. Run the following command to start both Elasticsearch and Kibana:

   ```bash
   docker-compose up 
   ```
5. Once the services are up and running:
   - Access Elasticsearch at: http://localhost:9200
   - Access Kibana at: http://localhost:5601


## Data Persistence
Elasticsearch stores its data in a volume mounted to ./esdata on the host machine, ensuring data persistence across container restarts.

## Stopping the Services
To stop the services, press Ctrl + C or run:
``` 
docker-compose down
```
This will stop and remove the containers but preserve the data.

