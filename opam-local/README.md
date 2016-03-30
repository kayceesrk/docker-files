# Dockerfile for opam-local development

## Build

```
$ docker build -t opam-local .
```

## Run

```
$ docker run -it opam-local
opam@7b7b22c6e27e:~$ opam  --version
1.3.0~dev3
```

## Update

To fetch the latest commits from `opam local` development branch:

```
$ docker run -it opam-local
opam@7b7b22c6e27e:~$ git clone https://github.com/inhabitedtype/opam
opam@7b7b22c6e27e:~$ cd opam
opam@26ca36dfc98c:~/opam$ git checkout local
opam@26ca36dfc98c:~/opam$ ./configure && make lib-ext && make && sudo make install
```

The container now has all the latest commits. You can update the original image
as follows. Open a terminal on the host machine and find the name of the running
container.

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
898528cf8b04        opam-local          "bash"              2 minutes ago       Up 2 minutes                            sharp_murdock
```

The name of the running container is `sharp_murdock` in this case. Update the docker image as:

```
$ docker commit -m "Update opam-local" sharp_murdock opam-local:latest
```

The `opam-local` image is now updated with the latest changes. If you spin up
the image again, you should see the latest changes:

```
$ docker run -it opam-local
opam@898528cf8b04:~$ ls
opam
```

## Develop

You can also mount your opam development repo (located at `$(PWD)/opam` on your host machine) in the container as follows:

```
$ docker run -it -v $(PWD)/opam:/opam opam-local
```

You can now build opam in the container.

```
opam@7b7b22c6e27e:~$ cd /opam/
opam@7b7b22c6e27e:/opam$ ./configure && make lib-ext && make && sudo make install
```
