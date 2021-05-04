FROM debian:stretch AS build

RUN apt-get update \
 && apt-get install -y --no-install-recommends build-essential ca-certificates git bison autoconf autogen automake libgcrypt20-dev \
 && git clone https://github.com/ldmud/ldmud.git
COPY doe_settings ldmud/src/settings
RUN cd ldmud/src && ./autogen.sh \
 && bash settings/doe_settings \
 && make install-driver

FROM debian:stretch

COPY --from=build /usr/local/bin/ldmud /usr/local/bin/ldmud

ADD driver.sh /usr/local/bin/

EXPOSE 4242 4246/udp
VOLUME /mud/lib

CMD [ "/usr/local/bin/driver.sh" ]
