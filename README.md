## Challenges

### Pihole and Traefik both use port 80

Pihole was first setup to use docker network host mode so that it can be reachable outside the host without messing with the lan routing. 
Traefik UI listens on port 80. I ended up mapping the container port to `8000` port on the host.

I need to specify the port when trying to reach the other containers, like so: `http://grafana.homelab.lan:8000/`
This works but is not ideal.


### Node Exporter was not picking host interface stats

Network metrics like `node_network_transmit_bytes_total` were pointing to the container interface instead of the host.
Which is weird considering that `node_network_up` showed all the host interfaces.

After unsucessfully trying some `path.rootfs` configurations and passing other optional commandline arguments, I bit the bullet
 and installed node exporter on the host.
