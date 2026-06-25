# Database-strategy
Сервис | База данных | Обоснование
------|:--------:|------:
Bidding Service     | Redis     | RTB требует latency < 80 ms. Используется in-memory хранение ставок и таргетинга
Campaign Service     | PostgreSQL     | ACID, управление кампаниями и креативами
Statistics Service    | Kafka + ClickHouse  | Высокоскоростная запись событий
Analytics Service     | ClickHouse  | OLAP-запросы и отчётность
Financial Service     | PostgreSQL  | Строгая консистентность финансовых операций

#### Bidding Service  
Почему Redis?

Для RTB недопустимо выполнять запросы к PostgreSQL на каждый bid request.

Текущая проблема:

Auction Engine
    →
PostgreSQL

Целевое состояние:
Bidding Service
    →
Redis

Средняя задержка:

Redis < 1 ms

#### Campaign Service

Использует PostgreSQL.

Хранит:
* кампании;
* креативы;
* настройки таргетинга;
* бюджетные ограничения.
* 
Требования:
* транзакционность;
* ссылочная целостность;
* сложные выборки.
* 
#### Statistics Service

Не хранит данные напрямую.
Функция:
Collect Event
 →
Kafka
 →
ClickHouse

#### Analytics Service

Использует ClickHouse.

Причины:
* миллиарды событий;
* высокая скорость агрегаций;
* колоночное хранение.
  
#### Financial Service

Использует PostgreSQL.

Требования:
* ACID;
* идемпотентность;
* аудит.
