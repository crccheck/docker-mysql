# My Dockerfile Pod

Written for Docker v0.6. I try to take advantage of [external volumes]. Like
Docker, these are only suitable for local development and are very much WIP.
DISCLAIMER: These should not be thought of as the right way to do things. I'm
just messing around trying to get things to work.

  [external volumes]: http://blog.docker.io/2013/07/docker-0-5-0-external-volumes-advanced-networking-self-hosted-registry/#external_volumes]


## How To Use These Recipes

These images are not on the [Index][docker index]. Mostly because I think these
`Dockerfile`s suck but also because the Docker index is currently a dumping
ground. You can build images yourself by following these instructions:

1. **Install Docker.** I strongly suggest following these [instructions] to avoid
   having to type `sudo docker`.
2. **Download this repo.** The simplest way is to use this one:
   `git clone https://github.com/crccheck/docker-pod.git && cd docker-pod`, but
   forking and contributing is encouraged!
3. **Build an image.** For example: `docker build -t mysql mysql/` builds
   `mysql/Dockerfile` and tags the image as `mysql`. You can see your images
   with: `docker images`.
4. **Use the image.** Each image has instructions on how to use it. They all
   sorta look like this: `docker run mysql`.

  [docker index]: https://index.docker.io/
  [instructions]: http://docs.docker.io/en/latest/use/basics/#why-sudo


## Have fun!

                                       ##         .
                                 ## ## ##        ==
                              ## ## ## ## ##    ===
                           /""""""""""""""""\___/ ===
                      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
                           \______ o          _,/
                            \      \       _,'
                             `'--.._\..--''

  [whale]:  https://gist.github.com/dhrp/5733652


----
# Dockerfile Documentation

## Postgresql 9.2 and Postgis 2.0

A Postgresql 9.2 + Postgis 2.0 image that supports external volumes.

### Example Usage

    docker run -d -p 5432:5432 -v ~/volumes/postgres/:/mnt/postgres/ postgis

References:
* https://github.com/orchardup/docker-postgresql/blob/master/Dockerfile
* http://www.ubuntuupdates.org/ppa/postgresql

## `mysql-server`

A mysql image (version 5.5 at the time of writing) that supports external
volumes. The login is `docker` with no password.

### Example Usage

Run in background on port 3306 storing files in `~/volumes/mysql`:

    docker run -d -p 3306:3306 -v ~/volumes/mysql:/mnt/mysql/ mysql

Fix fubar'd permissions in the remote volume:

    docker run -v ~/volumes/mysql:/mnt/mysql/ mysql sh /usr/local/bin/fix-permissions.sh

References:
* https://github.com/kstaken/dockerfile-examples/tree/master/mysql-server
* https://github.com/paulczar/docker-mysql/blob/master/Dockerfile
* http://dischord.org/blog/2013/08/13/docker-and-owncloud-part-2/

