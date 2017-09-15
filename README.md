# JOI Energy

## Overview

JOI Energy is a new energy company that uses data to ensure customers are 
able to be on the best tariff for their energy consumption.

## API

Below is a list of API endpoints with their respective input and output.

### Store Readings

#### Endpoint

```
POST
/readings/store
```

#### Input

```json
{
    "meterId": <meterId>,
    "electricityReadings": [
        { "time": <timestamp>, "reading": <reading> },
        ...
    ]
}
```

`timestamp`: Unix timestamp, e.g. `1504777098`   
`reading`: kW reading of meter at that time, e.g. `0.0503`

### Get Stored Readings

#### Endpoint

```
GET
/readings/read/<meterId>
```

`meterId`: A string value, e.g. `meter-0`

#### Output

```json
[
    { "time": "2017-09-07T10:37:52.362Z", "reading": 1.3524882598124337 },
    ...
]
```

### View Current Tariff and Compare Usage Cost Against all Tariffs

#### Endpoint

```
GET
/tariffs/compare-all/<meterId>
```

`meterId`: A string value, e.g. `meter-0`

#### Output

```json
{
    "tariff-id": "tariff-2",
    "tariff-comparisons": { 
        "tariff-0": 21.78133785680731809,
        ...
    }
}
```

### View Recommended Tariffs for Usage

#### Endpoint

```
GET
/tariffs/recommend/<meterId>[?limit=<limit>]
```

`meterId`: A string value, e.g. `meter-0`

`limit`: Limit to display only a number of tariffs, e.g. `2`

#### Output

```json
[
    { 
        "tariff-0": 15.084324881035297
    },
    ...
]
```

## Requirements

- [Java 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
- [Gradle](https://gradle.org/)

## Build

```console
$ gradle build
```

## Test

```console
$ gradle test # Run unit tests
$ gradle functionalTest # Run functional tests
```

## Run

```console
$ gradle run # available at localhost:8080 by default
```
