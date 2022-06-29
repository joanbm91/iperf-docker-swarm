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

   Modify /etc/haproxy/haproxy.cfg
   
   NOTE: On my running environment HAproxy is running on external server and not on the same docker-swarm server.
   
  you can add it if neccesary on the same docker-swarm cluster where the iperf service with the following configuration:
   ```
   haproxy:
    image: haproxy:latest
    volumes:
        - ./haproxy:/usr/local/etc/haproxy # route to configuration file haproxy.cfg
    ports:
        - "5202:5202"  
        - "5204:5204"
        - "5205:5205"
        - "5206:5206"
    expose:
        - 5202
        - 5204
        - 5205
        - 5206

        ```

3- Restart haproxy service
> service haproxy restart
 
