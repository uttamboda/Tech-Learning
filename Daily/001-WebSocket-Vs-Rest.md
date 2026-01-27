* Today i am learning new topic is websocket and restapi differance :

** WebSocket :
1)client open one conection
2)conection stay opne 
3)both saides can massages any time 
4)this is called full-duplex comunications

Example =
A chat app:
You connect once
Your friend types → message arrives instantly
You type → they see it instantly
No refreshing, no repeated requests

CommanUses :
Chat applications
Live notifications
Online games
Stock price updates
Collaborative tools (Google Docs-style)


** RestApi :
1)client sends request
2)server send a response 
3)conection close
4)Repeat every time you need new data
5)This usually happens over HTTP.

Example =
You open Instagram:
App → “Hey server, give me my feed”
Server → “Here you go”
Done.
You refresh:
App → “Hey again, anything new?”
Server → “Yep / Nope”
Done.

CommanUses :
Login / signup
Fetch user profile
Get a list of products
Submit a form