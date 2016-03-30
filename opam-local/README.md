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

You can also mount your opam development repo (located at `$(PWD)/opam` on your host machine) in the container as follows:

```
$ docker run -it -v $(PWD)/opam:/opam opam-local
```

You can now build opam in the container.

```
opam@7b7b22c6e27e:~$ cd /opam/
opam@7b7b22c6e27e:/opam$ ./configure && make lib-ext && make && sudo make install
```
