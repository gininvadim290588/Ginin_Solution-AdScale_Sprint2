# Масштабирование

## Репликация
#### Campaign DB
Primary

 ├─ Read Replica 1
 
 └─ Read Replica 2
Используется схема:
Write → Primary
Read → Replica

#### Finance DB
Primary

 └─ Standby Replica
 
Причина:
финансовые операции критичны к консистентности.

#### ClickHouse
Используется:
ReplicatedMergeTree

## Шардирование

#### Analytics
Шардирование по:
campaign_id

Причины:
высокая кардинальность;
равномерное распределение.

#### Statistics
Шардирование Kafka:

partition key = campaign_id

Bidding

Redis Cluster:

hash(campaign_id)

#### CQRS
Используется для аналитики.
##### Command Side
Campaign Service
Finance Service
##### Query Side
Analytics Service

События передаются через Kafka.
