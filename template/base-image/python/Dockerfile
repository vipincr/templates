FROM --platform=${TARGETPLATFORM:-linux/amd64} ghcr.io/openfaas/classic-watchdog:0.2.0 as watchdog
FROM --platform=${TARGETPLATFORM:-linux/amd64} python:3-alpine

ARG TARGETPLATFORM
ARG BUILDPLATFORM

# Allows you to add additional packages via build-arg
ARG ADDITIONAL_PACKAGE

RUN echo "http://dl-8.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog
RUN apk --no-cache add ca-certificates shadow \
                       jpeg-dev zlib-dev libjpeg postgresql-dev\
                       wget freetype-dev libpng-dev openblas-dev ${ADDITIONAL_PACKAGE} \
    && apk add --virtual build-deps gcc python3-dev musl-dev build-base linux-headers \
    && echo "session  optional  pam_umask.so" >> /etc/pam.d/base-session-noninteractive 

RUN ln -s /usr/include/locale.h /usr/include/xlocale.h
RUN pip install numpy scipy pandas matplotlib Pillow  && apk del build-deps
# Add non root user
RUN addgroup -S app && adduser app -S -G app -g "umask=0000"

CMD ["fwatchdog"]
