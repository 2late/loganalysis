# Assumptions
1. Web servers store records in text files. Each file can contain multiple records separated by new line. 
2. The files are written with rotation by time and volume.
3. jsonPayload will have the same structure/schema for all messages. jsonPayload.body field will not have a specific schema(type text).

# Diagram
![Diagram](Diagram.jpg?raw=true "Diagram")

# Description
1. Each web server will contain Kafka connector that can read JSON log file and ingest each JSON record into Kafka topic. It can also be a custom producer or producer script included in Kafka package.
2. Kafka cluster that hosts the topic for log records. Kafka cluster will be scaled to handle the volume.
3. Kafka consumer that will persist records from Kafka into a distributed storage for long term storage. The records will be persisted in compressed format. This part is optional.
4. Kafka connector or consumer that will write records from Kafka to ElasticSearch.
5. ElasticSearch will store log records and provide quick access and full text search capability.
6. Logs can be accessed via Kibana or ElasticSearch query API.

# Questions
## What kind of applications can you think of that could be made possible with your design?

If the question is about the capability that the design can add to the application, then any application that runs on production envirinment and require diagnostics and monitoring.

## What are the limitations or drawbacks of your design?
1. Kafka will persist all messages from the topic and will increase utilization of disk space.
2. The solution is scalable and it is good for large volume of logs. It may not be an optimal option for a small system that doesn't produce too many log messages.


