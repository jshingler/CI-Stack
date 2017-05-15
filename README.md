# CI-Stack

I took the docker compose and added Maven and Sonar.


## Instructions for Settin up Concourse CI

http://concourse.ci/docker-repository.html

NOTE: The keys `host_key` and `host_key.pub` should be renamed `tsa_host_key` and `tsa_host_key.pub` respectively.

```
    mkdir -p keys/web keys/worker

    ssh-keygen -t rsa -f ./keys/web/tsa_host_key -N ''
    ssh-keygen -t rsa -f ./keys/web/session_signing_key -N ''

    ssh-keygen -t rsa -f ./keys/worker/worker_key -N ''

    cp ./keys/worker/worker_key.pub ./keys/web/authorized_worker_keys
    cp ./keys/web/tsa_host_key.pub ./keys/worker
```

----------

# Setup

## Starting the CI-Stack
```
docker-compose up
```

## Docker Config
The stack is compose of several containers.  It requires additional Memory and CPU allocation.

Increase CPU to 6 and Memory to 4 GB.

![CPU Memory Settings](/resources/images/memory_cpu.png)
### AUFS Bug
There is an AUFS Bug that requires setting an advanced parameter.

![AUFS Setting](/resources/images/aufs.png)

## Docker Nexus SSL
We are running a Nexus container setup with SSL.  In our case, the container uses self signed certificates. In order to access the container, docker has to be configure with "insecure registries" on ports 8443, 18443, 18444.  See Below:

![Insecure Registry setup](/resources/images/insecure_registries.png)


## Nexus Config as Docker Registry

Setup

* docker-hub (Proxy) on port 18443 using remote url https://registry-1.docker.io
* docker-internal (Hosted) on port 18444
* docker (Group) containing docker-hub and docker-internal
