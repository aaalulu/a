This is an internal websocket server used to:
- handle the clients connection from the user's home web page
- receive the 1D/7D/30D top movers sent by the "top_movers.py" script (located in the "top_movers" folder)
- send the 1D/7D/30D top movers to the clients once they connect or once the "top_movers.py" script sent them to us (normally every hour)
- receive, every 5 minutes, a HTTP request from the connected clients to get the last coin news.  
	these news are retrieved from the API of thecoin.news website  
	(why the clients send us this HTTP request rather than querying thecoin.news API directly ? because this API doesn't allow cross origin (cors policy))