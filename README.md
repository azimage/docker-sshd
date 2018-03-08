Docker Image Packaging for SSHD
===============================

[![Travis](https://img.shields.io/travis/alvistack/docker-sshd.svg)](https://travis-ci.org/alvistack/docker-sshd)
[![GitHub release](https://img.shields.io/github/release/alvistack/docker-sshd.svg)](https://github.com/alvistack/docker-sshd/releases)
[![GitHub license](https://img.shields.io/github/license/alvistack/docker-sshd.svg)](https://github.com/alvistack/docker-sshd/blob/master/LICENSE)
[![Docker Pulls](https://img.shields.io/docker/pulls/alvistack/docker-sshd.svg)](https://hub.docker.com/r/alvistack/docker-sshd/)

OpenSSH is the premier connectivity tool for remote login with the SSH protocol. It encrypts all traffic to eliminate eavesdropping, connection hijacking, and other attacks. In addition, OpenSSH provides a large suite of secure tunneling capabilities, several authentication methods, and sophisticated configuration options.

Learn more about SSHD: <https://www.openssh.com/>

Overview
--------

This Docker container makes it easy to get an instance of SSHD up and running.

### Quick Start

Start SSHD:

    # Pull latest image
    docker pull alvistack/docker-sshd

    # Run as detach
    docker run \
        --name sshd \
        --publish 2222:22 \
        alvistack/docker-sshd

**Success**. SSHD is now available on port `2222`.

Because this container **DIDN'T** handle the generation of root password, so you should set it up manually with `pwgen` by:

    # Generate password with pwgen
    PASSWORD=$(docker exec -i sshd pwgen -cnyB1); echo $PASSWORD

    # Inject the generated password
    echo "root:$PASSWORD" | docker exec -i sshd chpasswd

Alternatively, you could inject your own SSH public key into container's authorized\_keys by:

    # Inject your own SSH public key
    (docker exec -i sshd sh -c "cat >> /root/.ssh/authorized_keys") < ~/.ssh/id_rsa.pub

Now you could SSH to it as normal:

    ssh root@localhost -p 2222

Versioning
----------

The `latest` tag matches the most recent version of this repository. Thus using `alvistack/docker-sshd:latest` or `alvistack/docker-sshd` will ensure you are running the most up to date version of this image.

License
-------

-   Code released under [Apache License 2.0](LICENSE)
-   Docs released under [CC BY 4.0](http://creativecommons.org/licenses/by/4.0/)

Author Information
------------------

-   Wong Hoi Sing Edison
    -   <https://twitter.com/hswong3i>
    -   <https://github.com/hswong3i>

