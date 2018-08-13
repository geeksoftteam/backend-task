---
title: TickerBase

search: false
---

# Introduction

1. Your task is to implement an API based on this documentation.
2. The API can be written in any framework you feel most comfortable with.
3. We do not give any deadline. Take your time and write as best code as you can.
4. Provide the solution with complete Git commits history.

### Things we care about

1. Code quality.

# Project Description

Imagine you are a broker employee and have been assigned a task to create a simple database collecting ticks (prices) for different currency pairs (like `EURUSD`, `PLNUSD` etc). First, save ticks manually using REST endpoint. Then, query these ticks based on dates in order to display them in the form of tick chart (chart containing all ticks collected throughout the day) and daily candles chart (containing daily intervals with max, min and average prices). The codename of this app will be: "TickerBase".

Good Luck!

<aside class="notice">
Attention! No login required, write an API without UI!
</aside>

# Ticks

## Create Tick

This endpoint saves the tick to database.

### HTTP Request

`POST http://example.com/api/ticks`

### Query Parameters

Parameter | Description
--------- | -----------
symbol | Symbol name like `EURUSD`, `BTCUSD`, `USDPLN`
price | Current price
timestamp | Timestamp of tick in milliseconds

<aside class="notice">
Please note that you don't have to get live currency pairs’ prices. Let's assume that another service connected to live price feed uses your API to store ticks to the database.
</aside>

## Get Ticks

```shell
curl "http://example.com/api/ticks/EURUSD?timestamp_from=1533831495547&timestamp_to=1533832497547"
```

> The above command returns JSON structured like this:

```json
[
  {
    "price": "1.1614",
    "timestamp": 1533831495547
  },
  {
    "price": "1.1617",
    "timestamp": 1533831497547
  },
  {
    "price": "1.1616",
    "timestamp": 1533832497547
  }
]
```

This endpoint queries database for ticks based on given interval with ascending order.

### HTTP Request

`GET http://example.com/api/ticks/{symbol}`

### Query Parameters

Parameter | Description
--------- | -----------
symbol | Queried symbol name
timestamp_from | Start of queried interval
timestamp_to | End of queried interval

# Candles

## Get Daily Candles

```shell
curl "http://example.com/api/candles/EURUSD"
```

> The above command returns JSON structured like this:

```json
[
  {
    "date": "2018-08-01",
    "min_price": "1.1670",
    "max_price": "1.1682",
    "avg_price": "1.1678"
  },
  {
    "date": "2018-08-02",
    "min_price": "1.1662",
    "max_price": "1.1667",
    "avg_price": "1.1675"
  }
]
```

This endpoint queries database for daily candles from current month. The candle is a structure containing daily minimum, maximum and average prices. The min, max, and average price is calculated based on all prices for a specified day.

### HTTP Request

`GET http://example.com/api/candles/{symbol}`

### Query Parameters

Parameter | Description
--------- | -----------
symbol | Queried symbol name
