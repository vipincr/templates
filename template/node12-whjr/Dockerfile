FROM --platform=${TARGETPLATFORM:-linux/amd64} vipinex/whjr-node:latest

# Turn down the verbosity to default level.
ENV NPM_CONFIG_LOGLEVEL warn

RUN chmod 777 /tmp

USER app

RUN mkdir -p /home/app/function

# Wrapper/boot-strapper
WORKDIR /home/app
COPY package.json ./

# This ordering means the npm installation is cached for the outer function handler.
RUN npm i

# Copy outer function handler
COPY index.js ./

# COPY function node packages and install, adding this as a separate
# entry allows caching of npm install

WORKDIR /home/app/function
COPY function/*.json ./

RUN npm i

# COPY function files and folders
COPY function/ ./

# Run any tests that may be available
RUN npm test

# Set correct permissions to use non root user
WORKDIR /home/app/

ENV cgi_headers="true"
ENV fprocess="node index.js"
ENV mode="http"
ENV upstream_url="http://127.0.0.1:3000"

ENV exec_timeout="10s"
ENV write_timeout="15s"
ENV read_timeout="15s"

ENV prefix_logs="false"

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

CMD ["fwatchdog"]
