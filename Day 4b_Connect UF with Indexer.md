Copy and paste the below configuration in the outputs.conf file of Universal Forwarder

outputs.conf

```bash
[tcpout]
defaultGroup=my_indexers

[tcpout:my_indexers]
server=YOUR_INDEXER_IP:9997

[tcpout-server://YOUR_INDEXER_IP:9997]
```

