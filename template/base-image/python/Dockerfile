FROM --platform=${TARGETPLATFORM:-linux/amd64} ghcr.io/openfaas/classic-watchdog:0.2.0 as watchdog
FROM --platform=${TARGETPLATFORM:-linux/amd64} python:3-alpine

ARG TARGETPLATFORM
ARG BUILDPLATFORM

# Allows you to add additional packages via build-arg
ARG ADDITIONAL_PACKAGE

RUN echo "http://dl-8.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

RUN echo "http://dl-cdn.alpinelinux.org/alpine/latest-stable/main" > /etc/apk/repositories
RUN echo "http://dl-cdn.alpinelinux.org/alpine/latest-stable/community" >> /etc/apk/repositories
RUN apk --no-cache --update-cache add ca-certificates shadow gcc gfortran build-base wget freetype-dev libpng-dev openblas-dev
RUN ln -s /usr/include/locale.h /usr/include/xlocale.h
RUN pip install pandas && addgroup -S app && adduser app -S -G app -g "umask=0000"

CMD ["fwatchdog"]
