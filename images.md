# mirror
- https://www.docker-cn.com/registry-mirror
- https://dev.aliyun.com/search.html
- https://hub.alauda.cn/

# systemVersions
- now: 2017-09-08 12:41:45
- preferred: FROM debian:stretch-slim
- in_use: python:2.7-stretch

## debian  ==> docker pull debian:stretch
- https://www.debian.org/releases/
- https://hub.docker.com/r/_/debian/
- FROM scratch
- ADD rootfs.tar.xz / # 26640844
- latest: [debian:stretch](https://github.com/debuerreotype/docker-debian-artifacts/blob/97dc072ae1e6c66c1ccc71ead334ce5d5fc201f0/stretch/Dockerfile)

## ubuntu ==> docker pull ubuntu:16.04
- https://hub.docker.com/_/ubuntu/
- FROM scratch
- ADD ubuntu-xenial-core-cloudimg-amd64-root.tar.gz /
- dev: [17.10 artful](https://github.com/tianon/docker-brew-ubuntu-core/blob/a2573609340194bf33712c1fa2dc4de8f9b70ca2/artful/Dockerfile)
- rolling: [17.04 zesty](https://github.com/tianon/docker-brew-ubuntu-core/blob/a2573609340194bf33712c1fa2dc4de8f9b70ca2/zesty/Dockerfile)
- latest(longteamsupport) : [16.04 xenial](https://github.com/tianon/docker-brew-ubuntu-core/blob/a2573609340194bf33712c1fa2dc4de8f9b70ca2/xenial/Dockerfile) # 46121166

## centos ==> docker pull centos:centos7
- FROM scratch
- ADD centos-7-docker.tar.xz / # 41941960
- latest: [centos7](https://github.com/CentOS/sig-cloud-instance-images/blob/3bcede00b70b87e870c48b449d89ac5ad96269d5/docker/Dockerfile?spm=5176.1972344.1.5.460ba2b8bJ4uOm)

## windows ==> docker pull microsoft/windowsservercore
- https://hub.docker.com/r/microsoft/windowsservercore/

## buildpack-deps ==> docker pull buildpack-dep:stretch || docker pull buildpack-dep:xenial
- https://hub.docker.com/_/buildpack-deps/
- From debian:stretch
- latest [stretch](https://github.com/docker-library/buildpack-deps/blob/5d86449454958f224035b5b200bfd3be9c088ff3/stretch/Dockerfile)
- FROM ubuntu:xenial
- buildpack-dep:xenial (buildpack-dep:xenial)[https://github.com/docker-library/buildpack-deps/blob/5d86449454958f224035b5b200bfd3be9c088ff3/xenial/Dockerfile]

## python ==> docker pull python:3.6-stretch|| docker pull python:2.7-stretch
- https://hub.docker.com/_/python/
- latest: 3.6-jessie
- FROM buildpack-deps:stretch
- python:2.7-stretch: [2.7](https://github.com/docker-library/python/blob/d3c5f47b788adb96e69477dadfb0baca1d97f764/2.7/stretch/Dockerfile)
- https://hub.docker.com/_/django/

	FROM python:3.4

	RUN apt-get update \
	    && apt-get install -y --no-install-recommends \
	        postgresql-client \
	    && rm -rf /var/lib/apt/lists/*

	WORKDIR /usr/src/app
	COPY requirements.txt ./
	RUN pip install -r requirements.txt
	COPY . .

	EXPOSE 8000
	CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]


## redis ==> docker pull redis-4.0
- https://hub.docker.com/_/redis/
- FROM debian:jessie-slim
- latest: [4.0.1](https://github.com/docker-library/redis/blob/1d6d5acf99aedd42aa0195ad5f22b8ffa6841f96/4.0/Dockerfile)

## mysql ==> docker pull mysql:5.7
- https://hub.docker.com/_/mysql/
- FROM debian:jessie
- latest: [5.7.19](https://github.com/docker-library/mysql/blob/0590e4efd2b31ec794383f084d419dea9bc752c4/5.7/Dockerfile)

## rabbitmq ==> docker pull rabbitmq:3.6
- https://hub.docker.com/_/rabbitmq/
- FROM debian:stretch-slim
- latest: (3.6.13)[https://github.com/docker-library/rabbitmq/blob/7d76799247764423a69438f72961ef0581788e07/3.6/debian/Dockerfile]
- I'm using rabbitmq-server-3.6.6-1.el6.noarch.rpm

## others
- https://hub.docker.com/_/registry/
- https://hub.docker.com/_/busybox/
- https://hub.docker.com/_/nginx/
- https://hub.docker.com/_/mongo/
- https://hub.docker.com/_/elasticsearch/
- https://hub.docker.com/_/haproxy/

# images
- use for container and should keep stabale(RO)

# layer
- every modify directive will create new layer(RO)
- docker history  debian:stretch 

# container
- when dealing with dockfile, all change write to the container(RW)
- container’s writable layer
- container’s volume