# Lambda Triggers

Orbs Lambda supports 3 types of triggers: OnSchedule, onBlocks, onEvent.

See [interfaces.ts](https://github.com/orbs-network/orbs-lambda/blob/master/interfaces.ts) for the full description of types and definitions.   

## OnSchedule
Allows you to trigger your task based on a predefined schedule, either a cron expression or an "every x" notation.
Interface:
```js
onSchedule(
    fn, // function to execute
    schedule, // cron expression / every x minutes/hours/days
    network, // string representation of one of the supported networks
    config // key:value object
)
```

### Cron Expression
Standard cron expression in UTC timezone.

Format:
```
 *    *    *    *    *
┬    ┬    ┬    ┬    ┬
│    │    │    │    |
│    │    │    │    └ day of week (0 - 7) (0 or 7 is Sun)
│    │    │    └───── month (1 - 12)
│    │    └────────── day of month (1 - 31)
│    └─────────────── hour (0 - 23)
└──────────────────── minute (0 - 59)
```

Examples with the cron format:

42 * * * *
 : _Execute when the minute is 42 (e.g. 19:42, 20:42, etc.)._

0 0 * * 1 : _Execute at 00:00 on Monday_

#### Unsupported Cron Features

Currently, `W` (nearest weekday) and `L` (last day of month/week) are not supported.
Most other features supported by popular cron implementations should work just fine,
including `#` (nth weekday of the month).

[cron-parser](https://github.com/harrisiirak/cron-parser) is used to parse crontab instructions.


### "Every" notation
If you don't like writing cron expressions and prefer to configure your job to run every nth minute/hour/day.
Starting time used as reference is the first minute of the hour / first hour of the day / first day of the month, respectively.

(TODO)

Format: [number]m|h|d

Examples: 

"5m" = every 5th minute of the hour, starting from xx:00 (e.g. 04:00, 04:05, 04:10...)

"3h" = every 3rd hour, starting from 00:00. (e.g. 00:00, 03:00, 06:00...)

"7d" = At 00:00 on every 7th day-of-month, starting on the 1st (e.g. 2022-09-01 00:00:00, 2022-09-08 00:00:00, 2022-09-15 00:00:00, 2022-09-22 00:00:00, 2022-09-29 00:00:00, 2022-10-01 00:00:00)

## onBlocks
Runs on consecutive block ranges and lets you apply your own logic on this range.

Interface:
```js
onBlocks(
    fn, // function to execute
    network, // string representation of one of the supported networks
    config // key:value object
)
```

## onEvent

TODO

## Subscribing to triggers
In order to subscribe to one or more of the triggers above, one must implement and export a "register" function.

```js
module.exports.register = function (engine) {
    engine.onSchedule(myEthTask, "0 0 * * 1", 'ethereum', configEth)
    engine.onSchedule(myPolygonTask, "12h", 'polygon', configPolygon)
    engine.onBlocks(....)
```

In the above example, after implementing `myEthTask` and `myPolygonTask` functions, we bind them to trigger handlers.
- Don't worry about the `engine` object. It is provided by the backend process on run-time.
- You may bind each of your task functions to one or more handlers. This gives you the flexibility, for example, to run the same task on different networks with different configuration.