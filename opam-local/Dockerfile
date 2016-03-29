# opam-local for debian-stable with local switch of OCaml 4.02.3
FROM ocaml/ocaml:debian-stable
LABEL distro_style="apt" distro="debian" distro_long="debian-stable" arch="x86_64" ocaml_version="4.02.3" operatingsystem="linux"
RUN apt-get -y update && \
  DEBIAN_FRONTEND=noninteractive apt-get -y upgrade && \
  DEBIAN_FRONTEND=noninteractive apt-get -y install aspcud && \
	git clone https://github.com/inhabitedtype/opam /tmp/opam && \
  sh -c "cd /tmp/opam && git checkout local && make cold && make install && rm -rf /tmp/opam" && \
  echo 'opam ALL=(ALL:ALL) NOPASSWD:ALL' > /etc/sudoers.d/opam && \
  chmod 440 /etc/sudoers.d/opam && \
  chown root:root /etc/sudoers.d/opam && \
  adduser --disabled-password --gecos '' opam && \
  passwd -l opam && \
  chown -R opam:opam /home/opam
USER opam
ENV HOME /home/opam
WORKDIR /home/opam
RUN mkdir .ssh && \
  chmod 700 .ssh && \
  git config --global user.email "opam-local@inhabitedtype.com" && \
  git config --global user.name "opam-local" && \
  sudo -u opam sh -c "opam init -y && opam switch 4.02.3"
RUN sudo -u opam sh -c "printf '\n. /home/opam/.opam/opam-init/init.sh > /dev/null 2> /dev/null || true\n' >> .bashrc"
RUN sudo apt-get -y install vim emacs
CMD [ "bash" ]
