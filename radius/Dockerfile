FROM freeradius/freeradius-server:latest
MAINTAINER Djan <djan.iffan@gmail.com>

LABEL Description="freeradius Docker based on Ubuntu 20.04 LTS" \
	License="GPLv2" 

ENV DEBIAN_FRONTEND noninteractive

# default timezone
ENV TZ Asia/Jakarta

RUN apt-get update \
	&& apt-get install --yes --no-install-recommends \
		apt-utils \
		ipcalc \
		tzdata \
		net-tools \
		mariadb-client \
		libmysqlclient-dev \
		unzip \
		wget \
		nano \
	&& rm -rf /var/lib/apt/lists/*

# Create directories
# /data should be mounted as volume to avoid recreation of database entries
RUN mkdir /app /data /internal_data
WORKDIR /app

# Copy init script to image
ADD ./init-freeradius.sh /app

# Make init.sh script executable
RUN chmod +x /app/init-freeradius.sh

# Expose FreeRADIUS Ports
EXPOSE 1812 1813

# Run the script which executes freeradius in foreground
CMD ["/app/init-freeradius.sh"]
ENTRYPOINT ["/app/init-freeradius.sh"]