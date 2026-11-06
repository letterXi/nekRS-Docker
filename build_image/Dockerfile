FROM ubuntu:24.04

ARG USER_ID=1000
ARG GROUP_ID=1000

RUN apt-get update && \
	apt-get install -y build-essential libopenmpi-dev cmake git wget

RUN userdel -r ubuntu && groupadd -g $GROUP_ID nekRS && \
	useradd -m nekRS -u $USER_ID -g $GROUP_ID

USER nekRS

WORKDIR /home/nekRS

RUN git clone https://github.com/Nek5000/nekRS.git && cd nekRS && \
	yes "" | CC=mpicc CXX=mpic++ FC=mpif77 ./build.sh -DCMAKE_INSTALL_PREFIX=$HOME/.local/nekrs && \
	mkdir project && \
	rm -r nekRS

ENV NEKRS_HOME=/home/nekRS/.local/nekrs
ENV PATH=/home/nekRS/bin:$PATH

