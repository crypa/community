# Signal Structure & Types

## Condition Types
### Above & Below
This is very basic and common math symbols for a strategy.
- ```"type": "above"``` will equal to ```source > value```
- ```"type": "below"``` will equal to ```source < value```

### Cross Above & Cross Below
- ```"type": "cross_above"``` will equal to ```source[0] > value & source[1] < value```
- ```"type": "cross_below"``` will equal to ```source[0] < value & source[1] > value```

### Highs & Lows
When there is a higher High, in another words when the price closed higher than the day before, this is a signal of greater confidence and a possible trend for further higher prices. On the flip side when there is a lower Low, this suggests that confidence is lowering and the price will fall.
 ```rust
// Source will be a array of <hh = 2 | hl = 1 | lh = -1 | ll = -2>
for i in <iterations>:
    if source[i+<offset>] != <value>
        return false
return true
```
- ```"type": "higher_high"``` will equal to `2`
- ```"type": "higher_low"``` will equal to `1`
- ```"type": "lower_high"``` will equal to `-1`
- ```"type": "lower_low"``` will equal to `-2`
```json
{
    "type": "<type>",

    // The offset is the amount to offset back in history.
    "offset": 1,

    // Amount of times the type should be true, default 1.
    "iterations": 2
}
```
### Flag
This is the way to use flag signals in buy and sell signals, the flag type is only allowed in buy and sell signals.

#### Example
```json
{
    "type": "flag",
    "loopback_period": 20,
    "flag": "<flag_key>",
    "value": true
}
```



## Signal Structure
```json
{
    "<signal_type>": {
        "<signal_key>": {
            // Check if the signal is enabled, default: true <Optional>
            // This value is also allowed to be a string e.g. "enable": "true" or "enable": "$use_sma_signal"
            // using a property from the properties section.
            "enable": true,

            // The display name of the strategy, default: "<signal_key>" <Optional>
            "name": "Simple Moving Average",

            
            "conditions": [
                {
                    "type": "above",

                    // The offset is the amount of candles to go back in history.
                    "offset": 10,

                    "value": 100
                }
            ]
        }
    }
}

```

## Flag Signal