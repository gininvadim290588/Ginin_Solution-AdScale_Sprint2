# Отказоустойчивость данных

#### RPO / RTO
Сервис      RPO      RTO
Bidding      0 мин   5 мин
Campaign  15 мин  30 мин
Statistics    0 мин   15 мин
Analytics    1 час    1 час
Finance      0 мин   15 мин

#### Backup Strategy
##### PostgreSQL
ежедневный Full Backup;
WAL Archiving;
Point-In-Time Recovery.
##### ClickHouse
ежедневные snapshots;
репликация между узлами.
##### Kafka
Replication Factor:
3
Min ISR:
2
##### Redis
Используются:
Redis Sentinel
+
Redis Cluster