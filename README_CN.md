
# API交易

## 1 说明


####  API 请求服务地址
    
`暂未上线`

####  签名方式
申请 API 将获得 accessKey 和 secretKey，先用sha加密secretKey，然后根据加密过的secretKey把请求的参数签名，请求参数按照ascii值排序加密，通过md5填充16位加密
### [示例代码](https://github.com/BitCola/quantitative/blob/master/src/main/java/com/bitcola/quantitative/api/TradeApi.java)

####  访问限制

每个接口每秒限制调用 5 次

### [错误码](https://github.com/BitCola/API-docs/blob/master/README_CN.md#5-%E9%94%99%E8%AF%AF%E7%A0%81)


## 2 配置

    
#### 服务器时间
```
GET /api/market/timestamp
```





> 返回示例

```json
{
    "status": 1000,
    "message": "success",
    "data": 1561443070237
}
```
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data`|string|服务器时间戳|
|`status`|number||
|`message`|string||
#### 配置
```
GET /api/market/config
```





> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.pair`|string|交易对|
|`data.amountScale`|number|数量精度|
|`data.priceScale`|number|价格精度|
## 3 市场

    
#### 获取 ticker 数据
```
GET /api/market/ticker
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`pair`|string|是|交易对|ETH_USDT|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.pair`|string|交易对|
|`data.vol`|string|24 小时成交量|
|`data.open`|string|24 小时开盘价|
|`data.close`|string|最新成交价|
|`data.high`|string|24 小时最高价|
|`data.low`|string|24 小时最低价|
#### 所有 ticker 数据
```
GET /api/market/AllTicker
```





> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.pair`|string|交易对|
|`data.vol`|string|24 小时成交量|
|`data.open`|string|24 小时开盘价|
|`data.close`|string|最新成交价|
|`data.high`|string|24 小时最高价|
|`data.low`|string|24 小时最低价|
#### 获取深度
```
GET /api/market/depth
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`pair`|string|是|交易对|ETH_USDT|
|`size`|integer|否|长度，默认 100，最大 100|2|
|`merge`|integer|否|价格合并，默认为交易对 priceScale，最小为 priceScale - 3，最大为 priceScale|0|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.ask`|array|卖方深度[价格,数量]|
|`data.bids`|array|买方深度[价格,数量]|
#### 最新成交
```
GET /api/market/trades
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`pair`|string|是|交易对|ETH_USDT|
|`size`|integer|否|返回最新条数，默认20，最大 100|2|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.price`|number|价格|
|`data.number`|number|数量|
|`data.direction`|string|方向|
|`data.timestamp`|number|成交时间|
#### k 线
```
GET /api/market/kline
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`pair`|string|是|交易对|ETH_USDT|
|`type`|string|是|1m/5m/15m/30m/1h/4h/6h/8h/12h/1d|1m|
|`endTimestamp`|number|否|k 线截止时间，默认为服务器当前时间|1561384440000|
|`size`|integer|否|返回数据长度|1|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data`|array|[时间戳,开,高,低,收,成交量]|
## 4 交易

    
#### 委托下单
```
GET /api/trade/order
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`accessKey`|string|是||accessKey|
|`amount`|number|是|数量|99|
|`direction`|string|是|方向|buy|
|`pair`|string|是|交易对|NXT_USDT|
|`price`|number|是|价格|100|
|`reqTime`|number|是|请求时间（毫秒）|1561695795677|
|`type`|string|是|下单类型，目前只支持 LIMIT|LIMIT|
|`sign`|string|是|签名|8fef38cf548c3c639eff92914acf6b80|




> 返回示例

```json
{
    "status": 1000,
    "message": "success",
    "data": "1561443070237"
}
```
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data`|string|订单 ID|
#### 取消委托
```
GET /api/trade/cancelOrder
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`accessKey`|string|是||accessKey|
|`id`|string|是|订单 ID|1144462404485959680|
|`reqTime`|number|是||1561696191547|
|`sign`|string|是||98beddad85269b6f79bda169705e1abc|





#### 获取订单
```
GET /api/trade/getOrder
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`accessKey`|string|是||accessKey|
|`id`|string|是|订单 ID|1144462404485959680|
|`reqTime`|number|是||1561696726670|
|`sign`|string|是||8ce4d660ce738d8046ea20f4570eb340|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.id`|string|订单 ID|
|`data.pair`|string|交易对|
|`data.direction`|string|下单方向|
|`data.timestamp`|number|下单时间戳|
|`data.price`|number|下单价格|
|`data.number`|number|下单数量|
|`data.remain`|number|未成交数量|
|`data.status`|string|订单状态|
|`data.type`|string|订单类型|
#### 获取账户信息
```
GET /api/trade/getAccountInfo
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`accesskey`|string|是||accessKey|
|`reqTime`|number|是||1561694265429|
|`sign`|string|是||9fa4448b77f3905754e58971797cc4db|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.balances.coinCode`|string|币种名称|
|`data.balances`|array|账户信息|
|`data.balances.available`|number|可用资金|
|`data.balances.frozen`|number|冻结资金|
|`data.balances.unitDecimal`|number|币种精度|
#### 获取订单列表
```
GET /api/trade/getOrders
```

>Query
    
|参数名|类型|必需|描述|示例|
|---------|-------|-------------|-------|---|
|`accessKey`|string|是||accessKey|
|`direction`|string|否|下单方向|buy|
|`page`|number|是|页数|1|
|`pair`|string|是|交易对| BTC_USDT|
|`reqTime`|number|是||1561696726670|
|`status`|string|否|订单状态|PENDING|
|`type`|string|否|订单类型|LIMIT|
|`sign`|string|是||8ce4d660ce738d8046ea20f4570eb340|




> 返回示例

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
> 返回参数
    
|参数名|类型|描述|
|--|--|--|
|`data.id`|string|订单 ID|
|`data.pair`|string|交易对|
|`data.direction`|string|下单方向|
|`data.timestamp`|number|下单时间戳|
|`data.price`|number|下单价格|
|`data.number`|number|下单数量|
|`data.remain`|number|未成交数量|
|`data.status`|string|订单状态|
|`data.type`|string|订单类型|

## 5 错误码
