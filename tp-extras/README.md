## TP Extras
*By Josse DE OLIVEIRA* \
[Go Back](../README.md)

### Load Balancer
I create a new Apache configuration:
```conf
<VirtualHost *:80>
    ServerName localhost
    ProxyPreserveHost On
    ProxyPass / http://tp1-frontend-srv:80/
    ProxyPassReverse / http://tp1-frontend-srv:80/
</VirtualHost>

Header add Set-Cookie "ROUTEID=.%{BALANCER_WORKER_ROUTE}e; path=/" env=BALANCER_ROUTE_CHANGED
<Proxy "balancer://back">
    BalancerMember "http://tp1-backend-srv1:8080" route=1
    BalancerMember "http://tp1-backend-srv2:8080" route=2
    ProxySet stickysession=ROUTEID
</Proxy>

Listen 8080

<VirtualHost *:8080>
    ServerName localhost
    ProxyPreserveHost On
    ProxyPass / "balancer://back/"
    ProxyPassReverse / "balancer://back/"
</VirtualHost>

LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so
LoadModule slotmem_shm_module modules/mod_slotmem_shm.so
LoadModule proxy_balancer_module modules/mod_proxy_balancer.so
LoadModule lbmethod_byrequests_module modules/mod_lbmethod_byrequests.so
```

This image is build by github with the tag `:extras`, and can be used with `playbook-extra.yaml` that launches multiple backends

With this starategy, if we stop `tp-backend-srv1`, `tp-backend-srv2` will be used. If we restart it, `tp-backend-srv2` will still be used. `tp-backend-srv1` will be used only if `tp-backend-srv2` is taken down. This strategy may not be optimal, but it can be changed.

