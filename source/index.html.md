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

Image you are a broker and want to create a simple database for ticks (prices)
for different currency pairs (like `EURUSD`, `PLNUSD` etc). You will save the ticks
manually using REST endpoint. You need to query these ticks based on
dates to display them on chart and you also need daily candles (max, min and
average values of prices). The codename for this app will be: "TickerBase".

Good Luck!

<aside class="notice">
Remember! No login required. Write just the API, without UI!
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
Please note that you don't have to get real prices of currencies pairs. Let's assume
that another service which is connected to real feed of prices will use your API
to store the ticks to database.
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

This endpoint queries database for daily candles from current month.
Candle is a structure aggregated by day and containing minimum, maximum and average prices during that day.
Average is calculated by taking all prices during that day into consideration.

### HTTP Request

`GET http://example.com/api/candles/{symbol}`

### Query Parameters

Parameter | Description
--------- | -----------
symbol | Queried symbol name
