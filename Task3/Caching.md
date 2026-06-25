# Кэширование
#### Что кэшируем:

* Кампании
campaign:1001
* Ставки
bid:1001
* Таргетинг
targeting:1001
* Бюджеты
budget:1001

#### Где расположен Redis
Campaign Service
       →
Redis Cluster
       →
Bidding Service

#### TTL

Кампании 10 мин;
Таргетинг 10 мин;
Ставки      5 мин;
Бюджеты  30 сек;

#### Инвалидация
При изменении кампании:
Campaign Updated
 →
Kafka
 →
Redis

Update
Используется:
Cache Aside

#### Cache Warming
После рестарта:

Campaign DB
 →
Campaign Service
 →
Redis

Предзагрузка:
активных кампаний;
ставок;
таргетингов.
