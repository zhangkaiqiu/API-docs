### 
# API-docs
[中文文档](https://github.com/BitCola/API-docs/blob/master/README_CN.md)

## 1 Introduction


####  API Server Address
    
`Not yet open`

####  Signature
`Applying API will get accessKey and secretKey, first encrypt the secretKey with sha, then sign the requested parameters according to the encrypted secretKey, request parameters are sorted and encrypted according to ascii value, and 16-bit encryption is filled by md5`
### [Example](https://github.com/BitCola/quantitative/blob/master/src/main/java/com/bitcola/quantitative/api/TradeApi.java)

####  Limit

`5 calls per second per API`

### [Error Code](https://github.com/BitCola/API-docs#5-error-code)


## 2 Configuration

    
#### server time
```
GET /api/market/timestamp
```





> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": 1561443070237
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data`|string|timestamp|
|`status`|number||
|`message`|string||
#### Configuration
```
GET /api/market/config
```





> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": [
        {
            "pair": "ETH_USDT",
            "amountScale": 4,
            "priceScale": 2
        }
    ]
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.pair`|string||
|`data.amountScale`|number||
|`data.priceScale`|number||
## 3 Market

    
####  Ticker
```
GET /api/market/ticker
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`pair`|string|Y||ETH_USDT|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": {
        "pair": "ETH_USDT",
        "vol": "0.0000",
        "open": "189.36",
        "close": "189.36",
        "high": "189.36",
        "low": "189.36"
    }
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.pair`|string||
|`data.vol`|string||
|`data.open`|string||
|`data.close`|string||
|`data.high`|string||
|`data.low`|string||
#### All Ticker
```
GET /api/market/AllTicker
```





> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": [
        {
            "pair": "ETH_USDT",
            "vol": "0.0000",
            "open": "189.36",
            "close": "189.36",
            "high": "189.36",
            "low": "189.36"
        },
        {
            "pair": "BTC_USDT",
            "vol": "0.0000",
            "open": "7063.95",
            "close": "7063.95",
            "high": "7063.95",
            "low": "7063.95"
        }
    ]
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.pair`|string||
|`data.vol`|string||
|`data.open`|string||
|`data.close`|string||
|`data.high`|string||
|`data.low`|string||
#### Depth
```
GET /api/market/depth
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`pair`|string|Y||ETH_USDT|
|`size`|integer|N|Default 100,Max 100|2|
|`merge`|integer|N|Default priceScale，Min priceScale - 3，Max priceScale|0|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": {
        "ask": [
            [
                194,
                1.398
            ],
            [
                193,
                13.4083
            ]
        ],
        "bids": [
            [
                188,
                2.332
            ],
            [
                186,
                12.7151
            ]
        ]
    }
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.ask`|array|sell[price,amount]|
|`data.bids`|array|buy[price,amount]|
#### Trades
```
GET /api/market/trades
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`pair`|string|Y||ETH_USDT|
|`size`|integer|N|Default 20，Max 100|2|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": [
        {
            "price": 191.24,
            "number": 0.0846,
            "direction": "buy",
            "timestamp": 1561444401960
        },
        {
            "price": 191.24,
            "number": 0.5058,
            "direction": "buy",
            "timestamp": 1561444401960
        }
    ]
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.price`|number||
|`data.number`|number||
|`data.direction`|string||
|`data.timestamp`|number||
#### Kline
```
GET /api/market/kline
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`pair`|string|Y||ETH_USDT|
|`type`|string|Y|1m/5m/15m/30m/1h/4h/6h/8h/12h/1d|1m|
|`endTimestamp`|number|N|Default server time|1561384440000|
|`size`|integer|N|Default 1000, Max 2000|1|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": [
        [
            1561444500000,
            191.24,
            191.24,
            191.24,
            191.24,
            0
        ]
    ]
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data`|array|[time,open,high,low,close,vol]|
## 4 Trade

    
#### Make Order
```
GET /api/trade/order
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`accessKey`|string|Y||accessKey|
|`amount`|number|Y||99|
|`direction`|string|Y||buy|
|`pair`|string|Y||NXT_USDT|
|`price`|number|Y||100|
|`reqTime`|number|Y||1561695795677|
|`type`|string|Y||LIMIT|
|`sign`|string|Y||8fef38cf548c3c639eff92914acf6b80|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": "1561443070237"
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data`|string|Order ID|
#### Cancel Order
```
GET /api/trade/cancelOrder
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`accessKey`|string|Y||accessKey|
|`id`|string|Y|Order ID|1144462404485959680|
|`reqTime`|number|Y||1561696191547|
|`sign`|string|Y||98beddad85269b6f79bda169705e1abc|





#### Get Order
```
GET /api/trade/getOrder
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`accessKey`|string|Y||accessKey|
|`id`|string|Y|Order ID|1144462404485959680|
|`reqTime`|number|Y||1561696726670|
|`sign`|string|Y||8ce4d660ce738d8046ea20f4570eb340|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": {
        "id": "1144462404485959680",
        "pair": "NXT_USDT",
        "direction": "buy",
        "timestamp": 1561696082293,
        "price": 100,
        "number": 9900,
        "remain": 9801,
        "status": "FULL_CANCELLED",
        "type": "LIMIT"
    }
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.id`|string|Order ID|
|`data.pair`|string||
|`data.direction`|string||
|`data.timestamp`|number||
|`data.price`|number||
|`data.number`|number||
|`data.remain`|number||
|`data.status`|string||
|`data.type`|string||
#### Account
```
GET /api/trade/getAccountInfo
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`accesskey`|string|Y||accessKey|
|`reqTime`|number|Y||1561694265429|
|`sign`|string|Y||9fa4448b77f3905754e58971797cc4db|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": {
        "balances": [
            {
                "coinCode": "USDT",
                "available": 4999940.0177,
                "frozen": 0,
                "unitDecimal": 4
            }
        ]
    }
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.balances.coinCode`|string||
|`data.balances`|array||
|`data.balances.available`|number||
|`data.balances.frozen`|number||
|`data.balances.unitDecimal`|number||
#### Orders
```
GET /api/trade/getOrders
```

>Query
    
|Field|Data Type|Require|Description|Example|
|---------|-------|-------------|-------|---|
|`accessKey`|string|Y||accessKey|
|`direction`|string|N||buy|
|`page`|number|Y||1|
|`pair`|string|Y|| BTC_USDT|
|`reqTime`|number|Y||1561696726670|
|`status`|string|N||PENDING|
|`type`|string|N||LIMIT|
|`sign`|string|Y||8ce4d660ce738d8046ea20f4570eb340|




> Return

```json
{
    "status": 1000,
    "message": "success",
    "data": [
        {
            "id": "1144462404485959680",
            "pair": "NXT_USDT",
            "direction": "buy",
            "timestamp": 1561696082293,
            "price": 100,
            "number": 9900,
            "remain": 9801,
            "status": "FULL_CANCELLED",
            "type": "LIMIT"
        }
    ]
}
```
> Return Field
    
|Field|Data Type|Description|
|--|--|--|
|`data.id`|string||
|`data.pair`|string||
|`data.direction`|string||
|`data.timestamp`|number||
|`data.price`|number||
|`data.number`|number||
|`data.remain`|number||
|`data.status`|string||
|`data.type`|string||

## 5 Error Code
