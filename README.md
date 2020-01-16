# Assumptions
1. Web servers store records in text files. Each file can contain multiple records separated by new line. The files are written rotation by time and volume.

# Diagram
![Diagram](Diagram.jpg?raw=true "Diagram")

# Description
1. Each web server will contain Kafka connector that can read JSON log file  and ingest each JSON record into Kafka topic. It can also be a custom producer or producer script included in Kafka package.
2. Kafka cluster that hosts the topic for log records. Kafka cluster will be scaled to handle the volume.
3. Kafka consumer that will persist records from Kafka into a distributed storage for long term storage. The records will be persisted in compressed format.
4. Kafka connector or consumer that will write records from Kafka to ElasticSearch.
5. ElasticSearch will store log records and provide quick access and full text search capability.
6. Logs can be accessed via Kibana or custom backend.
