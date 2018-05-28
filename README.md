# poist-javascript-client
This is an example of connecting to poist using javascript.

# Connecting

```
<script src="//cdnjs.cloudflare.com/ajax/libs/sockjs-client/1.1.2/sockjs.min.js"></script>
<script src="stomp.js"></script>
<script type="text/javascript">
 var ws = new SockJS("http://your-ip:15674/stomp");
 var client = Stomp.over(ws);
 
 client.heartbeat.outgoing = 0;
 client.heartbeat.incoming = 0;
 
 var onConnect = function() {
   client.subscribe("/topic/messages", function(d) {
   var str = d.body
   var res = str.match(/Body:\'(.+)\'/);
   console.log("I control this",res[1]);
   });
 };
 
 var onError = function(e) {
   console.log("ERROR", e);
 };
 
 client.connect("admin", "adminpassword", onConnect, onError, "/");
 
</script>
```
