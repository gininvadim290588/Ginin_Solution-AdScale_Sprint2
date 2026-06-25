# Выбор Gateway

Kong Gateway

Причины:
* быстро внедряется;
* поддерживает rate limiting;
* поддерживает OAuth/JWT;
* поддерживает observability.

Основные функции:

##### Маршрутизация

/openrtb/bid
↓
Ad Server

#### Rate Limiting

Ограничение запросов DSP.
Например, 20000 RPS на одного партнёра.

#### Аутентификация

Поддержка: API Key, JWT.

#### Мониторинг
Сбор: RPS; P95; P99; ошибки.

####  Circuit Breaker

При деградации Bidding Service:
Closed
 ↓
Open
 ↓
Half Open