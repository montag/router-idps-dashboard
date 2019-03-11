# https://github.com/elastic/logstash-docker
FROM docker.elastic.co/logstash/logstash:6.6.1

USER root
RUN yum groupinstall -y 'Development Tools' \
    && yum install -y libcurl-devel zlib-devel \
    && mkdir /root/maxmind \
    && cd /root/maxmind \
    && git clone https://github.com/maxmind/geoipupdate \
    && cd geoipupdate \
    && ./bootstrap \
    && ./configure \
    && make \
    && make install \
    # && echo "ProductIds GeoLite2-City GeoLite2-Country 506 517 533" >> /usr/local/etc/GeoIP.conf \
    && geoipupdate \
    # Add your logstash plugins setup here
    && logstash-plugin install logstash-filter-translate \
    && logstash-plugin install logstash-filter-dns
