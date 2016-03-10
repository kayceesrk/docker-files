FROM ocaml/opam:debian
#Perf
RUN sudo apt-get -y install flex bison wget linux-tools
RUN wget https://github.com/torvalds/linux/archive/v4.1.tar.gz && \
		tar xzf v4.1.tar.gz && \
		make -C linux-4.1/tools/perf && \
		mkdir -p .local/install && \
		make -C linux-4.1/tools/perf O=$HOME/.local/install
#Editors
RUN sudo apt-get -y install vim emacs
#OCaml tools
RUN sudo -u opam sh -c "opam depext -u merlin utop tuareg" && \
    sudo -u opam sh -c "opam install -y -j 2 -v merlin utop tuareg"
#RR
RUN sudo apt-get -y install ccache cmake make g++-multilib gdb \
     pkg-config libz-dev realpath python-pexpect manpages-dev git zlib1g-dev
RUN git clone https://github.com/mozilla/rr && \
	  cd rr && mkdir obj && cd obj && \
		cmake .. && make -j8 && \
		sudo make install
