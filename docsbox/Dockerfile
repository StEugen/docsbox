FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update 
RUN apt-get install -y tzdata && \
    ln -fs /usr/share/zoneinfo/Europe/Samara /etc/localtime && \
    dpkg-reconfigure --frontend noninteractive tzdata && \
    apt-get clean

RUN apt-get update
RUN apt-get install -y libffi-dev libmagic-dev libmagickwand-dev
RUN apt-get install -y libreoffice libreofficekit-dev
RUN apt-get install -y python3-dev python3-pip git
RUN apt-get install -y python3-magic
RUN apt-get clean
RUN apt-get install -y locales
RUN locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


ADD . /home/docsbox
WORKDIR /home/

RUN pip3 install --upgrade pip
RUN pip3 install -r docsbox/requirements.txt

ENTRYPOINT ["gunicorn", "-b", ":8001", "docsbox:app"]
