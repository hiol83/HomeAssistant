FROM resin/rpi-raspbian:stretch
MAINTAINER hassio

COPY qemu-arm-static /usr/bin/qemu-arm-static

RUN apt-get update && apt-get -y install apt-transport-https wget ca-certificates apt-utils gnupg libzip4 libavahi-client3 libavahi-client-dev insserv

RUN \
    touch /tmp/HOMEGEAR_STATIC_INSTALLATION; \
    wget https://apt.homegear.eu/Release.key && apt-key add Release.key && rm Release.key; \
    echo 'deb https://apt.homegear.eu/Debian/ stretch/' >> /etc/apt/sources.list.d/homegear.list; \
    apt-get update && apt-get -y install homegear homegear-management homegear-webssh homegear-adminui homegear-nodes-core homegear-nodes-extra homegear-homematicbidcos homegear-max homegear-influxdb vim less htop; \
    rm -f /etc/homegear/dh1024.pem; \
    rm -f /etc/homegear/homegear.crt; \
    rm -f /etc/homegear/homegear.key; \
    cp -R /etc/homegear /etc/homegear.config; \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
	
COPY start.sh /start.sh
COPY main.conf /etc/homegear.config/main.conf
COPY rpcservers.conf /etc/homegear.config/rpcservers.conf
COPY php.ini /etc/homegear.config/php.ini
RUN chmod +x /start.sh
ENTRYPOINT ["--platform linux/arm/v7", "/bin/bash", "-c", "/start.sh"]

EXPOSE 2001 2002 2003
