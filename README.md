# iperf

Deploy from a swarm manager node:


> sudo docker stack deploy --compose-file docker-compose.yml iperf3-haproxy

# How add more iperf servers

1- Stop docker stack

> docker stack ls
> 
> docker stack rm "stack-name"

1- Modify the docker-compose file adding more iperf servers running on different port

2- Modify the proxyserver serving requests
    
    - devproxypre01 (development -> swarm dev cluster)
    - devproxypro01 (production -> swarm pro cluster)
   Modify /etc/haproxy/haproxy.cfg

3- Restart haproxy service
> service haproxy restart
 