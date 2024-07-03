FROM woodpeckerci/woodpecker-agent:next-b8b6efb352-alpine

ENV WOODPECKER_SERVER=creature-swift.internal:9000
ENV WOODPECKER_HEALTHCHECK=false
ENV WOODPECKER_GRPC_SECURE=false
ENV WOODPECKER_HOSTNAME=creature-swift-agent.internal:3000
ENV WOODPECKER_HEALTHCHECK_ADDR=creature-swift-agent.internal:3000
ENV WOODPECKER_MAX_WORKFLOWS=1

ENV WOODPECKER_BACKEND=local

RUN apk add --no-cache git git-lfs bash curl nodejs gcompat wget ca-certificates

RUN mkdir -p /tmp
RUN chmod 1777 /tmp

# Install Bun
RUN curl -fsSL https://bun.sh/install | bash
# Verify Bun installation
RUN chmod -R 755 /root/.bun

# Install fly cli
RUN curl -L https://fly.io/install.sh | sh

RUN export PATH=${PATH}:$(ls -d /tmp/woodpecker-local-*/home/.fly)
ENV PATH=${PATH}:/root/.bun/bin

# https://github.com/oven-sh/bun/issues/5545
# Install glibc to run Bun
RUN if [[ $(uname -m) == "aarch64" ]] ; \
    then \
    # aarch64
    wget https://raw.githubusercontent.com/squishyu/alpine-pkg-glibc-aarch64-bin/master/glibc-2.26-r1.apk ; \
    apk add --no-cache --allow-untrusted --force-overwrite glibc-2.26-r1.apk ; \
    rm glibc-2.26-r1.apk ; \
    else \
    # x86_64
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.28-r0/glibc-2.28-r0.apk ; \
    apk add --no-cache --allow-untrusted --force-overwrite glibc-2.28-r0.apk ; \
    rm glibc-2.28-r0.apk ; \
    fi


EXPOSE 3000

ENTRYPOINT ["/bin/woodpecker-agent"]