### How to use:
```bash
python top_movers.py
```

need to set up a cron every hour

need to configure some settings in top_movers.py file:
- debug
- internal_websocket_server_url
- logos_folder_path


### What it is:
- retrieves the markets from FTX and Binance and filter them to keep only the futures/spots with a USD/USDT quote preferably
	(there are more than 700 markets from FTX, after filtering there are less than 200. as for Binance it's more than 1500 markets 
	reduce to a little bit more than 200. so in the end that's arround 400 markets, with a majority of duplicate markets)
- get the last 30 days candles of theses 400 markets with one hour interval (that represents 721 candles by market)
- calcul the percentage fluctuation of each market for the last 1 day / 7 days / 30 days with one hour precision
	so if the time is monday 4pm:
		- the 1 day fluctuation is the comparaison of the open price of the current hour candle with the open price of the candle of the day before at 4pm. 
		- the 7 days fluctuation is the comparaison with the 4pm candle open price 7 days ago (the last monday).
		- the 30 days fluctuation is the comparaison with the 4pm candle open price 30 days ago
- the percentage fluctuations are sorted based on their greatest absolute value (whatever they greater or less than 0, so -70% is higher than +60%).
	and then these FTX and Binance fluctuations are combined to keep only the top 5 for each 1D/7D/30D
- the final 1D/7D/30D tops 5 are sent to an internal websocket server (located in "golang_ws" folder)