## Get Strategies
- URL : ``/api/strategies``
 - Method : ``GET``
 - URL Params : none
 - Data Params
 - Success Response
	 - Code : 200
	 - Content
 ```json
[
  {
    "name": "CCI",
    "params": "# constant multiplier. 0.015 gets to around 70% fit\nconstant = 0.015\n\n# history size, make same or smaller than history\nhistory = 90\n\n[thresholds]\nup = 100\ndown = -100\npersistence = 0"
  },
  {
    "name": "DEBUG_single-advice",
    "params": ""
  },
  {
    "name": "DEBUG_toggle-advice",
    "params": ""
  },
  {
    "name": "DEMA",
    "params": "weight = 21\n\n[thresholds]\ndown = -0.025\nup = 0.025\n"
  },
  {
    "name": "MACD",
    "params": "short = 10\nlong = 21\nsignal = 9\n\n[thresholds]\ndown = -0.025\nup = 0.025\npersistence = 1"
  },
  {
    "name": "PPO",
    "params": "short = 12\nlong = 26\nsignal = 9\n\n[thresholds]\ndown = -0.025\nup = 0.025\npersistence = 2"
  },
  {
    "name": "RSI",
    "params": "interval = 14\n\n[thresholds]\nlow = 30\nhigh = 70\npersistence = 1"
  },
  {
    "name": "StochRSI",
    "params": "interval = 3\n\n[thresholds]\nlow = 20\nhigh = 80\npersistence = 3"
  },
  {
    "name": "TMA",
    "params": "short = 7\nmedium = 25\nlong = 99\n"
  },
  {
    "name": "TSI",
    "params": "short = 13\nlong = 25\n\n[thresholds]\nlow = -25\nhigh = 25\npersistence = 1"
  },
  {
    "name": "UO",
    "params": "[first]\nweight = 4\nperiod = 7\n\n[second]\nweight = 2\nperiod = 14\n\n[third]\nweight = 1\nperiod = 28\n\n[thresholds]\nlow = 30\nhigh = 70\npersistence = 1\n"
  },
  {
    "name": "custom",
    "params": "my_custom_setting = 10"
  },
  {
    "name": "noop",
    "params": ""
  },
  {
    "name": "talib-macd",
    "params": "[parameters]\noptInFastPeriod = 10\noptInSlowPeriod = 21\noptInSignalPeriod = 9\n\n[thresholds]\ndown = -0.025\nup = 0.025"
  },
  {
    "name": "tulip-adx",
    "params": "historySize = 80\noptInTimePeriod = 15\ncandleSize = 10\n\n[thresholds]\nup = 30\ndown = 20"
  },
  {
    "name": "tulip-macd",
    "params": "[parameters]\noptInFastPeriod = 10\noptInSlowPeriod = 21\noptInSignalPeriod = 9\n\n[thresholds]\ndown = -0.025\nup = 0.025"
  },
  {
    "name": "tulip-multi-strat",
    "params": "optInTimePeriod = 2\noptInFastPeriod = 4\noptInSlowPeriod = 7\noptInSignalPeriod = 23.707189677282354\n\ncandleSize = 1\nhistorySize = 4\n\nup = 24.52\ndown = 55.74\nmacd_up = 14.498233170768081\nmacd_down = -9.65220944122072\n"
  },
  {
    "name": "varPPO",
    "params": "momentum = \"TSI\" # RSI, TSI or UO\n\n[thresholds]\nweightLow = 120\nweightHigh = -120\n\n# How many candle intervals should a trend persist\n# before we consider it real?\npersistence = 0"
  }
]
```
 - Error Response : none
 - Call
 ``router.get('/api/strategies', require('local/dir/strategies')); ``

## Get "ConfigPart"
- URL
``/api/configPart/:part``
 - Method
 ``GET``
 - URL Params
	 - Required
         ``part = 'paperTrader' or 'candelWriter' or 'performanceAnalyzer'``
 - Data Params
  none
 - Success Response
	 - Code : 200
	 - Content
		 - paperTrader
``{"part": "feeMaker = 0.25\nfeeTaker = 0.25\nfeeUsing = 'maker'\nslippage = 0.05\n\n[simulationBalance]\nasset = 1\ncurrency = 100\n" }`` 
		- candleWriter
			``{"part":"enabled = true\nadapter = \"sqlite\""}``
		- performanceAnalyzer
``{"part":"# Used to calculate sharpe ratio\n# yearly % of riskfree return for example\n# treasury bonds or bank interest.\n\nriskFreeReturn = 2"}``
 - Error Response
	 - Code : 200
	 - Content : ``error :(``
 - Call
  ``router.get('/api/configPart/:part', require('local/dir/configPart')));``

## Get API Keys
- URL : 
``/api/apiKeys``
 - Method : 
 ``GET``
 - URL Params 
 none
 - Data Params 
 none
 - Success Response
	 - Code : 200
	 - Content : (*example; empty if no API keys saved*) 
	 ``["poloniex", "gdax"]``
 - Error Response 
 none
 - Call
 ``router.get('/api/apiKeys', require(ROUTE('local/dir/apiKeys')))``
 - Notes
	 - It appears that the JSON only returns the exchange names in an list, presumably the literal keys are hidden from REST implementation.

## Get Imports
- URL
 ``/api/imports``
 - Method
 ``GET``
 - URL Params
 none
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (*example*)
```json
[
  {
    "watch": {
      "exchange": "poloniex",
      "currency": "USDT",
      "asset": "BTC"
    },
    "id": "254834834128682",
    "latest": "2018-06-11T20:46:58Z",
    "from": "2018-03-11 21:17",
    "to": "2018-06-11 21:17",
    "done": true
  }
]
 ```
 - Error Response
	none
 - Sample Call
``router.get('/api/imports', (ctx, next) => {});``

## Get Running "Gekkos" (Running trade bots, paper or real)
- URL
- ``/api/gekkos``
 - Method
 ``GET``
 - URL Params
none
 - Data Params
 none
 - Success Response
	 - Code : 200
	 - Content (*example*)
```json
[
  {
    "watch": {
      "exchange": "gdax",
      "currency": "USD",
      "asset": "LTC"
    },
    "id": "249270745859179",
    "startAt": "2018-06-11T01:01:56Z",
    "latest": "2018-06-11T22:47:02Z",
    "mode": "realtime",
    "type": "watcher",
    "firstCandle": {
      "start": "2018-06-11T01:01:00.000Z",
      "open": 104.78,
      "high": 104.78,
      "low": 104.75,
      "close": 104.75,
      "vwp": 104.7664932330549,
      "volume": 18.18927793,
      "trades": 2
    },
    "lastCandle": {
      "start": "2018-06-11T22:46:00.000Z",
      "open": 105.54,
      "high": 105.67,
      "low": 105.51,
      "close": 105.67,
      "vwp": 105.64127875100343,
      "volume": 46.216300000000004,
      "trades": 24
    }
  },
```
 - Error Response
none
 - Sample Call
  ``router.get('/api/gekkos', listWraper('gekkos'));``


## Get Exchanges
- URL
``/api/exhanges``
 - Method
 ``GET``
 - URL Params
 none
 - Data Params
 none
 - Success Response
	 - Code : 200
	 - Content :  <em>See file : GetExchanges.md</em>
 - Error Response
 none
 - Sample Call
	``router.get('/api/exchanges', require('local/dir/exchanges')));``

## ADD API Key
- URL
``/api/addApiKey``
 - Method
``POST``
 - URL Params
	 - Required
	 - Optional none
 - Data Params
 none
 - Success Response
	 - Code : 200
	 - Content 
```json 
	 {"status":"ok"}
```
 - Error Response
	 - Code : 405
	 - Content 
	 `` 'Method Not Allowed' ``
 - Sample Call
 ``router.post('/api/addApiKey', apiKeys.add);``

## Remove API Key
- URL
``/api/removeApiKey``
 - Method
 ``POST``
 - URL Params
 none
 - Data Params
 none
 - Success Response
	 - Code : 200
	 - Content
```json 
	 {"status":"ok"}
```
 - Error Response
 none
 - Sample Call
	``router.post('/api/removeApiKey', apiKeys.remove);``

## Start a Scan
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/scan', require(ROUTE('scanDateRange')));

## Title
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/scansets', require(ROUTE('scanDatasets')));

## Title
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/backtest', require(ROUTE('backtest')));

## Title
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/import', require(ROUTE('import')));

## Title
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/startGekko', require(ROUTE('startGekko')));

## Title
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/killGekko', require(ROUTE('killGekko')));

## Title
- URL
 - Method
 - URL Params
	 - Required
	 - Optional
 - Data Params
 - Success Response
	 - Code : 200
	 - Content (JSON)
 - Error Response
	 - Code
	 - Content
 - Sample Call
 - Notes

router.post('/api/getCandles', require(ROUTE('getCandles')));