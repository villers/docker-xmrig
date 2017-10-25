# docker-xmrig
[XMRig miner](https://github.com/xmrig/xmrig) in an Alpine Linux Docker image.

The goal of this project is to quickly enable you to mine Monero without the hassle of knowing how to install or secure your mining software. 

Using an [Alpine Linux](https://www.alpinelinux.org/) container you get a very lightweight image ~4MB and the benefit of Alpine Linux's security model.
I have also configured this image to run the miner as a dedicated  restricted user.

# How to use
```bash
# docker run --restart unless-stopped --read-only -m 50M -c 512 villers/docker-xmrig -o POOL01 -u WALLET -p PASSWORD -k
# docker run --restart unless-stopped --read-only -m 50M -c 512 villers/docker-xmrig -o pool.supportxmr.com:80 -u 424y8KDstVH66NNbQ8BwUX3yy5jPnGva1F6FC8ryjHL7QREn5nycuhBP4hJWRt3znLEgawNw8BELQ2FDAyGmvzCB2okPBjz -p worker:email -k
# docker run -d --restart unless-stopped --read-only -m 50M -c 512 villers/docker-xmrig -a cryptonight-lite -o mine.aeon-pool.com:80 -u WmszCjp6bneaAerR9fXCGoDFrx8j1PKH9YU4g8W96TTFBF2XTL2tnh7hFaaEttMUt9c61Em6dP1WeHkyDtyRgWf11Q6QJzbAU -k
```
## Docker Arguments
`--restart unless-stopped`

If the miner crashes we want the docker service to restart it.

`--read-only`

This image does not need rw access.
If there are bug/exploits in the pool/software you are a little more protected.

`-m 50M`

Restricts memory usage to 50MB.

`-c 512`

By default XMRig will use <= half of your cores.
Setting a relevant share count will protect you from a runaway process locking your system.

## XMRig Arguments
`--help`

All standard XMRig arguments are supported, using `--help` will list all of them.
```bash
# docker run villers/docker-xmrig --help
```
`-t` 

When manually setting threads with `-t` you need to configure the correct CPU shares for docker.

IE if you have 4 cores each core is worth 256 `( 1024 / 4 )` and so to use 3 threads, CPU shares will need to be set to 756.
```bash
# docker run -c 756 villers/docker-xmrig ... -t 3
```

# Donations
XMR: `424y8KDstVH66NNbQ8BwUX3yy5jPnGva1F6FC8ryjHL7QREn5nycuhBP4hJWRt3znLEgawNw8BELQ2FDAyGmvzCB2okPBjz`
AEON: `WmszCjp6bneaAerR9fXCGoDFrx8j1PKH9YU4g8W96TTFBF2XTL2tnh7hFaaEttMUt9c61Em6dP1WeHkyDtyRgWf11Q6QJzbAU`
