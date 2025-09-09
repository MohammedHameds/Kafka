# Kafka-Data-Pipeline

Gold prices Api to Postgres

---

## 📌 Project Summary

- 🔄 **Source**: MySQL database named `ecomm`
- 🎯 **Sink**: PostgreSQL database named `ecomm`
- 🔌 **Connectors Used**:
  - **MySQL Source Connector** for capturing CDC events
  - **PostgreSQL Sink Connector** for writing to the destination
- 📦 **Plugins**: Uploaded to Kafka Connect for enabling connector functionality
- 📍 **Next Step**: Add support for **multiple sinks** (e.g., MongoDB, Elasticsearch) to fan out the data stream

---

## ⚙️ Technologies Used

- Apache Kafka
- Kafka Connect
- MySQL
- PostgreSQL
- Docker & Docker Compose

---

## 🚀 How to Run

1. **Clone the repository and go to the working directory**  

   > 💡 *Make sure Docker Desktop or Docker Engine is running before continuing.*
   ```bash

   make sure to install kafka on pthon pip install kafka-python

   docker compose -f api.yaml up -d

   docker ps
   ```
   
## 📋 Included Services

| Service | Port | Description | Access URL |
|---------|------|-------------|------------|
| **Kafka Broker**    | 9092        | Apache Kafka broker with KRaft mode              | `localhost:9092`            |
| **Schema Registry** | 8081        | Confluent Schema Registry                        | `http://localhost:8081`     |
| **Kafka Connect**   | 8083        | Kafka Connect for data integration               | `http://localhost:8083`     |
| **ksqlDB Server**   | 8088        | Stream processing with ksqlDB                    | `http://localhost:8088`     |
| **Kafka UI**        | 8090        | Web-based Kafka management interface             | `http://localhost:8090`     |
| **MySQL**           | 3306        | Source database for CDC (ecomm)                  | `localhost:3306`            |
| **PostgreSQL**      | 5432        | Sink database for CDC (admin)                    | `localhost:5432`            |
| **JMX Metrics**     | 1234, 1235  | Prometheus JMX metrics endpoints                 | -                           |
  
## 🔗 Connect to Databases via VS Code

You can connect to the MySQL and PostgreSQL containers using VS Code with a database extension like **Database Client** or **SQLTools**.

### 🐘 PostgreSQL Connection (Port: 5432)

| Field     | Value     |
|-----------|-----------|
| Host      | 127.0.0.1 |
| Port      | 5432      |
| Username  | admin     |
| Password  | password  |
| Database  | admin     |


## 🔌 Launch Kafka Connectors

After starting all services, run the following commands to deploy **PostgreSQL** connector:

### 🐘 Register PostgreSQL Connector
```bash
curl -sS -X POST \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  http://localhost:8083/connectors \
  -d @connectors/pg/pg-connect.json
```

### ✅ Verify Connectors Are Running
Open the following URL in your browser to check the status of both connectors:
```bash
http://localhost:8083/connectors?expand=status

$ curl -X DELETE http://localhost:8083/connectors/pg-connect 

```


