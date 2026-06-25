## Границы сервиса ставок

Bidding Service отвечает только за:
* выбор победителя аукциона;
* применение бизнес-правил;
* вычисление итоговой ставки;
* проверку лимитов кампаний;
* формирование Bid Response.

Не отвечает за:
* управление кампаниями;
* биллинг;
* аналитику;
* сбор статистики.

Контекст сервиса
DSP
 ↓
API Gateway
 ↓
Ad Server
 ↓ gRPC
Bidding Service
 ↓
Bid Response

Зависимости
*Синхронные*
Redis
Получение:
* ставок;
* таргетингов;
* активных кампаний.

*Асинхронные*
Kafka
Получение:
* campaign_updated;
* budget_updated.

Почему Redis?

В текущей системе Auction Engine ходит в PostgreSQL. Это главный bottleneck.
После выделения:
* PostgreSQL latency = 5-30 ms
* Redis latency = 0.1-1 ms

Снижение времени отклика достигает десятков миллисекунд.

#### API сервиса
##### gRPC
service BiddingService {

  rpc EvaluateBid(BidRequest)
      returns (BidResponse);

}

##### BidRequest
{
  "requestId":"123",
  "userId":"456",
  "placementId":"homepage",
  "device":"mobile"
}

##### BidResponse
{
  "campaignId":"1001",
  "creativeId":"5001",
  "bidPrice":1.25
}

#### Модель данных Redis

##### Campaign Cache
{
  "campaignId":1001,
  "status":"ACTIVE",
  "bid":1.25,
  "dailyBudget":5000,
  "targeting":"..."
}

##### Kafka Topics
* campaign_updated
* budget_updated
* campaign_paused
