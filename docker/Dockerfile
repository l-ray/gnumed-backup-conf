# Download base image ubuntu 22.04
FROM ubuntu:22.04
ARG DEBIAN_FRONTEND=noninteractive

RUN apt update && apt-get install -y postgresql postgresql-client gnupg software-properties-common && rm -rf /var/lib/apt/lists/*
RUN apt-key adv --recv-keys --keyserver keyserver.ubuntu.com FEE84259 && add-apt-repository ppa:gnumed/ppa
RUN apt update && apt-get install -y gnumed-server && rm -rf /var/lib/apt/lists/*
RUN service postgresql start && gm-bootstrap_server
RUN sed -i 's/\(local[ ]*all[ ]*all[ ]*peer\)/\1 map=root_as_gm-dbo/' /etc/postgresql/14/main/pg_hba.conf
RUN echo 'root_as_gm-dbo  root            gm-dbo' >> /etc/postgresql/14/main/pg_ident.conf

