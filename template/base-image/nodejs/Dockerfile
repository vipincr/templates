FROM --platform=${TARGETPLATFORM:-linux/amd64} ghcr.io/openfaas/of-watchdog:0.9.2 as watchdog
FROM --platform=${TARGETPLATFORM:-linux/amd64} node:12-alpine as ship

ARG TARGETPLATFORM
ARG BUILDPLATFORM

COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

RUN apk --no-cache add curl ca-certificates shadow python3 py3-pip \
    && echo "session  optional  pam_umask.so" >> /etc/pam.d/base-session-noninteractive \
    && addgroup -S app && adduser -S -G app -g "umask=0000" app

CMD ["fwatchdog"]