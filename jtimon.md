https://github.com/Juniper/jtimon
```
./jtimon --config config.json --print
```

```
# cat config.json
{
  "host": "10.102.140.59",
  "port": 50051,
  "cid": "tl-server01",
  "eos": true,
  "vendor": {
        "gnmi": {
            "encoding": "protobuf"
        }
  },
  "paths": [
        {
            "path": "/interfaces/interface",
            "freq": 10000
        },{
	    "path": "/components",
            "freq": 10000
        },{
            "path": "/qos",
            "freq": 10000
	},{
	     "path": "/network-instances/network-instance/protocols/protocol/bgp/neighbors/neighbor/state",
	     "freq": 10000
	},{
	     "path": "/network-instances/network-instance/protocols/protocol/bgp/neighbors/neighbor/afi-safis/afi-safi/state/prefixes",
	     "freq": 10000
   }],
   "log": {
	   "file": "jtimon.log"
    }
}
```
