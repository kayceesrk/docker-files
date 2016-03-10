FROM ocaml/opam:debian
#Perf
RUN sudo apt-get -y install flex bison wget linux-tools
RUN wget https://github.com/torvalds/linux/archive/v4.1.tar.gz && \
		tar xzf v4.1.tar.gz && \
		make -C linux-4.1/tools/perf
RUN sudo mv linux-4.1/tools/perf/perf /usr/bin/perf
#Editors
RUN sudo apt-get -y install vim emacs
#OCaml tools
RUN sudo -u opam sh -c "opam depext -u merlin utop tuareg" && \
    sudo -u opam sh -c "opam install -y -j 2 -v merlin utop tuareg"
