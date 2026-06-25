## Выбор протоколов взаимодействия
Взаимодействие | Протокол | Причина
------|:--------:|------:
DSP → Gateway     |HTTPS/OpenRTB     | Стандарт рынка
Gateway → Ad Server     |HTTP    |Простота
Ad Server → Bidding     | gRPC  | Минимальная задержка 
Campaign → Redis | Internal |Обновление кэша
Events → Kafka |Async | Высокая производительность
Analytics → Kafka | Async | Не влияет на RTB

Почему не REST между Ad Server и Bidding?
REST добавляет:
* сериализацию JSON;
* больший размер сообщений;
* дополнительные накладные расходы.

gRPC:
* HTTP/2;
* бинарный Protobuf;
* меньше latency.

Для RTB это критично.

Почему Kafka для событий?

Показы и клики:
* 18 000 RPS
* миллионы событий в день

Требования:
* высокая пропускная способность;
* буферизация;
* повторное чтение.

Kafka решает все три задачи.

##### Диаграмма взаимодействия
DSP
 ↓ 
Gateway
 ↓
Ad Server
 ↓ gRPC
Bidding Service
 ↓
Redis

Impression
 ↓
Event Service
 ↓
Kafka
 ↓
Analytics
