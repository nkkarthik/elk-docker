# Build with:
# docker build -t zoom/estationlogs .

# Run with:
# docker run -d --link elk:elk -v /mnt/estationlogs:/var/log --name estationlogs zoom/estationlogs

FROM debian:jessie

###############################################################################
#                                INSTALLATION
###############################################################################

### install Filebeat

RUN apt-get update -qq \
 && apt-get install -qqy curl \
 && apt-get clean


ADD ./filebeat /usr/bin/filebeat
RUN chmod +x /usr/bin/filebeat

###############################################################################
#                                CONFIGURATION
###############################################################################

### configure Filebeat

# config file
ADD filebeat.yml /etc/filebeat/filebeat.yml

# CA cert
RUN mkdir -p /etc/pki/tls/certs
ADD logstash-beats.crt /etc/pki/tls/certs/logstash-beats.crt

###############################################################################
#                                    START
###############################################################################

ADD ./start.sh /usr/local/bin/start.sh
RUN chmod +x /usr/local/bin/start.sh

CMD [ "/usr/local/bin/start.sh" ]

