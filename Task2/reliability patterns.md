# Паттерны надёжности

#### Circuit Breaker

Используется для вызовов:
* Ad Server → Bidding
* Ad Server → Redis
* Finance → Payment Gateway
Преимущества:
* предотвращение каскадных отказов;
* быстрое восстановление.
#### Retry + Exponential Backoff
Используется для:
* Kafka Producer
* Kafka Consumer
* Payment Gateway
Пример:
1 sec
2 sec
4 sec
8 sec

#### Timeout
Для RTB:
* Gateway → Ad Server = 20 ms
* Ad Server → Bidding = 15 ms
* Redis = 5 ms

Общий бюджет: < 80 ms
#### Fallback
Если Redis недоступен:
использовать локальный кэш последней версии кампаний.

Если Bidding Service недоступен:
вернуть заранее определённую безопасную ставку.

#### Идемпотентность финансовых операций
Каждая операция получает:
* transaction_id
Повторный запрос:
* same transaction_id
не приводит к повторному списанию.

