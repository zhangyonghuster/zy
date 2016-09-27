<h2> Amqp

+ reject the current RPC, if there is one
+ invalidate the channel object, meaning further operations will throw an exception
reject any RPCs waiting to be sent
+ cause the channel object to emit 'error'
+ cause the channel object to emit 'close'

<h4>error:

you can test it with require('amqplib/lib/connection').isFatalError(err) to see
if it was a crash-worthy error.


```
  #on('error', function (err) {...})
```

对close()事件的监听

```
  #on('close', function() {...})
```

```
#on('blocked', function(reason) {...})
```

```
#on('unblocked', function() {...})
```

A channel will emit 'error' if the server closes the channel for any reason. Such reasons include
```
#on('error', function(err) {...})
```

```
It's an error to supply a message that either doesn't require acknowledgement,
or has already been acknowledged. Doing so will errorise the channel.
If you want to acknowledge all the messages and you don't have a specific message around, 
use #ackAll.
```


A channel will not emit 'error' if its connection closes with an error.
```
#on('return', function(msg) {...})
```

Check that an exchange exists. If it doesn't exist, the channel will be closed with an error.
 If it does exist
```
#checkExchange(exchange, [function(err, ok) {...}])
```



<h5> option:

+ exclusive:if true, scopes the queue to the connection (defaults to false)
+ durable: if true, the queue will survive broker restarts, modulo the effects of exclusive and autoDelete;
 this defaults to true if not supplied, unlike the others
+ autoDelete: if true, the queue will be deleted
when the number of consumers drops to zero (defaults to false)
+ arguments: additional arguments, usually parameters for some kind of broker-specific extension e.g.,
high availability, TTL.


<h5> exchange

+ durable (boolean): if true, the exchange will survive broker restarts. Defaults to true.
+ internal (boolean): if true, messages cannot be published directly to the exchange (i.e., it can only be the target of bindings,
 or possibly create messages ex-nihilo). Defaults to false.
+ autoDelete (boolean): if true, the exchange will be destroyed once the number of bindings for
 which it is the source drop to zero. Defaults to false.
+ alternateExchange (string): an exchange to send messages to if
this exchange can't route them to any queues.
+ arguments (object): any additional arguments that may be needed by an exchange type.
