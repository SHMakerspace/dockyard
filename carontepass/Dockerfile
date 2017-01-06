#######################################################
# Dockerfile for carontepass at SHMakerspace
# Based on Ubuntu image
########################################################

# Set base image
FROM resin/rpi-raspbian:jessie-20160831
# Set file maintainer
MAINTAINER Chris Millar

# Set env variables used in this Dockerfile
ENV DOCKYARD_SRC=carontepass
#Directory inside container for all source files
ENV DOCKYARD_SRVHOME=/srv
# Directory in container for project source files
ENV DOCKYARD_SRVPROJ=/srv/carontepass

# update the default application repo source list
RUN apt-get update && apt-get -y upgrade

# Install python and crypt dependencies
RUN apt-get install -y python python-pip python-dev build-essential libffi-dev libssl-dev

# Create app subdirs
WORKDIR $DOCKYARD_SRVHOME
RUN mkdir media static logs
VOLUME ["$DOCKYARD_SRVHOME/media/", "$DOCKYARD_SRVHOME/logs", "$DOCKYARD_SRVHOME/static"]

# Copy Python Requirements to SRCDIR
COPY $DOCKYARD_SRC/requirements.txt $DOCKYARD_SRVHOME
RUN pip install -r $DOCKYARD_SRVHOME/requirements.txt

# Copy application source code to SRCDIR
COPY $DOCKYARD_SRC $DOCKYARD_SRVPROJ

# Port to expose
EXPOSE 8000

# Copy entrypoint script into the image
WORKDIR $DOCKYARD_SRVPROJ
COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]
