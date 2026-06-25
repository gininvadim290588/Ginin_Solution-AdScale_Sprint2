# Event-streaming
### Kafka Topics
* Кампании
campaign-created;
campaign-updated;
campaign-paused;
campaign-deleted;
* Финансы
budget-updated;
balance-updated;
payment-completed;
* RTB
bid-request;
bid-response;
* События
impression-created;
click-created;
conversion-created/

### Формат сообщений
Используется:
Apache Avro
Причины:
* компактность;
* контроль схем;
* совместимость версий.

Пример события
{
  "eventId":"123",
  "campaignId":"1001",
  "eventType":"impression",
  "timestamp":"2026-01-01T12:00:00Z"
}

### Consumer Groups
*Analytics
analytics-consumer-group
*Finance
finance-consumer-group
*Notification
notification-consumer-group
*Campaign
campaign-consumer-group


### Политика хранения
Impression 30 дней
Click 90 дней
Financial 365 дней
