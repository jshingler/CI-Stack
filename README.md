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


