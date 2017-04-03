FROM ubuntu
MAINTAINER Christian Schafmeister <meister@temple.edu>

# add full source repo into the 'app' user's $HOME/clasp
RUN mkdir foo
RUN echo "Hello there" >foo/dockertest.txt
#RUN mkdir /inside
RUN mount
RUN ls -ld /tmp/inside
RUN cp foo/dockertest.txt /tmp/inside/dockertest.txt