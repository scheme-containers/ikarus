# -*- mode: dockerfile; coding: utf-8 -*-
FROM debian:buster-slim AS build
RUN apt-get update && apt-get -y --no-install-recommends install \
      build-essential \
      bzr \
      ca-certificates \
      libffi-dev \
      libgmp-dev \
 && rm -rf /var/lib/apt/lists/*
WORKDIR /build
RUN bzr checkout --lightweight lp:ikarus
WORKDIR /build/ikarus
RUN ./configure
RUN make
RUN make install

FROM debian:buster-slim
RUN apt-get update && apt-get -y --no-install-recommends install \
      libffi6 \
      libgmp10 \
 && rm -rf /var/lib/apt/lists/*
COPY --from=build /usr/local/ /usr/local/
RUN ln -s ikarus /usr/local/bin/scheme-banner
CMD ["scheme-banner"]
