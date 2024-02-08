# MITM Proxy

* partial solution
    * sudo mitmweb -p 8881 --web-port 8882
    * chromium 'https://localhost:4040' --proxy-server="localhost:8881"
    * in brave go to http://localhost:8882/#/flows/34696f52-d1db-4648-b59a-94709e165956/request?s=oop
* revised solution
    * `mitmproxy -p 8081 -s ./replace.py --no-http2`
        * port 8081
        * use `replace.py` script
        * don't use http2 for tls (to make less secure so it can be rewritten)
    * configuration
        * in firefox about:profiles create a new profile
        * with mitmproxy running go to http://mitm.it/
        * download cert and install with directions
        * (will only work for that profile in firefox so safest way to install)

use replace.py config

```
http-server . -p 9000 & mitmproxy -p 8081 -s ./replace.py --no-http2 --ssl-insecure
```

replace.py

```python
'''Redirect HTTP requests to another server.'''
from mitmproxy import http
from mitmproxy import ctx

class MyConfig:
    def response(self, flow):
        h = flow.request.headers
        origin = h['origin'] if 'origin' in h else '*'
        flow.response.headers['Access-Control-Allow-Origin'] = origin

    def request(self, flow: http.HTTPFlow) -> None:
        ctx.log.info('>> ' + flow.request.pretty_host)

        if flow.request.path == 'path/to/rewrite':
            flow.request.host = 'localhost'
            flow.request.port = 9000
            flow.request.scheme = 'http'
            flow.request.path = '/proxy-data.json'
 

        if flow.request.method == 'OPTIONS':
            h = flow.request.headers
            origin = h['origin'] if 'origin' in h else '*'
            ctx.log.info('++ origin:' + origin);
            flow.response = http.HTTPResponse.make(200, b'', {
                'access-control-allow-credentials': 'true',
                'access-control-allow-origin': origin,
                'Access-Control-Allow-Methods': 'GET',
                'Access-Control-Allow-Headers': '*',
                'Access-Control-Max-Age': '1800',
                'Content-Type': 'application/json'
            })

addons = [
    MyConfig()
]
```



## Alternatives

* try resources override chome ext https://chrome.google.com/webstore/detail/resource-override/pkoacgokdfckfpndoffpifphamojphii

